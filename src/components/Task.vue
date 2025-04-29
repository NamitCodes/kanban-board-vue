<template>
    <div class="task" draggable="true" @dragstart="handleDragStart" :class="borderClass"
        @contextmenu.prevent="showContextMenu">
        <p class="task-text" contenteditable="true" ref="editable" @blur="updateTaskText"
            @keydown.enter.prevent="updateTaskText">{{ task.task_text }}</p>
    </div>
    <div v-if="showMenu" class="context-menu" :style="{ top: menuY + 'px', left: menuX + 'px' }">
        <ul>
            <li @click="deleteTask">🗑️</li>
        </ul>
    </div>
</template>

<script>
export default {
    props: ['task', 'columnId'],
    emits: ['delete-task'],
    methods: {
        handleDragStart(event) {
            const payload = {
                taskId: this.task.task_id,
                columnId: this.columnId
            };
            event.dataTransfer.setData("application/json", JSON.stringify(payload))
            // console.log(payload)
        },
        updateTaskText() {
            const updatedText = this.$refs.editable.innerText.trim();
            if (updatedText != "") {
                this.task.task_text = updatedText;
            } else {
                this.$refs.editable.innerText = this.task.task_text
            }
        },
        showContextMenu(event) {
            this.menuX = event.clientX;
            this.menuY = event.clientY;
            this.showMenu = true;

            document.addEventListener("click", this.hideContextMenu);
        },
        hideContextMenu() {
            this.showMenu = false;
            document.removeEventListener("click", this.hideContextMenu);
        },
        deleteTask() {
            const confirmed = window.confirm("Are you sure you want to delete this task?");
            if (confirmed) {
                this.$emit("delete-task", this.task.task_id);
                this.hideContextMenu(); // also close the menu
            }
        }
    },
    computed: {
        borderClass() {
            if (this.columnId === 1) {
                return "border-left-red"
            }
            else if (this.columnId === 2) {
                return "border-left-yellow"
            }
            else {
                return "border-left-green"
            }
        }
    },
    data() {
        return {
            showMenu: false,
            menuX: 0,
            menuY: 0
        }
    }

}
</script>

<style scoped>
.task {
    background-color: #fefefe;
    border-radius: 6px;
    margin-bottom: 10px;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
    /* Vue green for flair */
    padding: 0.5em;

    display: flex;
}

.task-text {
    padding: 0.5em;
    word-break: break-word;

    width: 100%;
}

.task-text:focus {
    outline: none;
}

.task-text:hover {
    background-color: #f0f0f0;
    /* cursor: text; */
}

.context-menu {
    position: fixed;
    background: white;
    border: 1px solid #ccc;
    z-index: 999;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
    border-radius: 4px;
}

.context-menu>ul {
    list-style-type: none;
    margin: 0;
    padding: 0.5em 0.5em;
}

.context-menu li {
    list-style-type: none;
    /* text-decoration: none; */
    margin: 0;
    padding: 0;
}

.context-menu ul:hover {
    background-color: #fc6060;
    cursor: pointer;
}





.border-left-red {
    border-left: 4px solid #b94242;
}

.border-left-green {
    border-left: 4px solid #42b983;
}

.border-left-yellow {
    border-left: 4px solid #c4c72d;
}
</style>
