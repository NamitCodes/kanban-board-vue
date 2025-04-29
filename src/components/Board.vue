<template>
    <div class="title">
        <h1>Kanban Board</h1>
    </div>
    <div class="board">
        <Column v-for="column in columns" :column="column" :key="column.col_id" @task-dropped="moveTask">
        </Column>
    </div>

</template>

<script>
import { compileScript } from 'vue/compiler-sfc';
import Column from './Column.vue';

export default {
    props: ['columns'],
    components: { Column },
    methods: {
        moveTask({ taskId, fromColumnId, toColumnId }) {
            const fromCol = this.columns.find(col => col.col_id === fromColumnId);
            const taskIndex = fromCol.tasks.findIndex(t => t.task_id === taskId);
            const task = fromCol.tasks[taskIndex]

            fromCol.tasks.splice(taskIndex, 1);

            const toCol = this.columns.find(col => col.col_id === toColumnId);

            toCol.tasks.push(task);
        }
    }
}
</script>

<style scoped>
.title {
    margin: 2rem;
}

.board {
    /* border: 2px solid black; */
    margin: 2rem;
    display: flex;
    justify-content: space-between;

    overflow: hidden;
}

@media (max-width: 550px) {
    .board {
        display: block;
    }
}
</style>