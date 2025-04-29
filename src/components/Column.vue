<template>
    <div class="column" @dragover.prevent @drop="handleDrop">
        <div class="column_title">
            <h2>{{ column.name }}</h2>
        </div>
        <Task v-for="task in column.tasks" :task="task" :key="task.task_id" :column-id="column.col_id"></Task>
    </div>

</template>

<script>
import Task from './Task.vue';

export default {
    props: ['column'],
    components: { Task },
    methods: {
        handleDrop() {
            const data = JSON.parse(event.dataTransfer.getData("application/json"))

            this.$emit('task-dropped', {
                taskId: data.taskId,
                fromColumnId: data.columnId,
                toColumnId: this.column.col_id
            });

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
</style>