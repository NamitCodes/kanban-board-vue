<template>
    <div class="title">
        <h1>Kanban Board</h1>
    </div>
    <div class="board">
        <Column v-for="column in columns" :column="column" :key="column.col_id">
        </Column>
    </div>

</template>

<script>
import Column from './Column.vue';

export default {
    props: ['columns'],
    components: { Column }
}
</script>

<style scoped>
.title {
    margin: 2rem;
}

.board {
    border: 2px solid black;
    margin: 2rem;
    display: flex;
    justify-content: space-between;
}

@media (max-width: 550px) {
    .board {
        display: block;
    }
}
</style>