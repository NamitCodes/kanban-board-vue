<template>
    <!-- <div class="column" @dragover.prevent @drop="handleDrop"> -->
    <div class="column" @touchend="handleDrop">
        <div class="column_title">
            <h2>{{ column.name }}</h2>
        </div>
        <!-- <Task 
        v-for="task in column.tasks" 
        :task="task" 
        :key="task.task_id" 
        :column-id="column.col_id"
        @delete-task="deleteTask"></Task> -->
        <draggable v-model="column.tasks" item-key="task_id" group="tasks" class="task-list">
            <template #item="{ element }">
                <Task :task="element" :column-id="column.col_id" @delete-task="deleteTask" />
            </template>
        </draggable>


        <form class="add-task" @submit.prevent="addTask">
            <input type="text" v-model="newTaskText" placeholder="Add a new task:">
            <!-- <button @click.prevent="addTask()" class="button">+</button> -->
        </form>
    </div>

</template>

<script>
import Task from './Task.vue';
import draggable from 'vuedraggable';

export default {
    props: ['column'],
    components: { Task, draggable },
    methods: {
        handleDrop() {
            const data = JSON.parse(event.dataTransfer.getData("application/json"))

            this.$emit('task-dropped', {
                taskId: data.taskId,
                fromColumnId: data.columnId,
                toColumnId: this.column.col_id
            });

        },
        addTask() {
            if (this.newTaskText !== "") {
                const newTask = {
                    task_id: Date.now(),
                    task_text: this.newTaskText
                }
                this.column.tasks.push(newTask)
                this.newTaskText = ""
            }
        },
        deleteTask(taskId) {
            this.column.tasks = this.column.tasks.filter(task => task.task_id !== taskId);
        }
    },
    data() {
        return {
            newTaskText: ""
        }
    }
}
</script>

<style scoped>
.column_title {
    /* border: 2px solid black; */
    font-style: 1vh;
    padding: 0 2em;
}

.column {
    /* border: 2px solid black; */
    padding: 2em;
    flex: 1;

    display: flex;
    flex-direction: column;

    background-color: #ffffff;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    margin: 0 1em;

    min-width: 0;
}

input[type=text] {
    border: none;
    border-bottom: 2px solid black;
    padding: 1em 1em 0 0;
    outline: none;
    font-size: 100%;
    width: 95%;
}
</style>