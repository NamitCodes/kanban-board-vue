<template>
    <div class="column">
        <div class="column_title">
            <h2>{{ column.name }}</h2>
        </div>
        <Task v-for="task in column.tasks" :task="task" :key="task.task_id"></Task>
    </div>

</template>

<script>
import Task from './Task.vue';

export default {
    props: ['column'],
    components: { Task }

}
</script>

<style scoped>
.column_title {
    border: 2px solid black;
    padding: 0 2em;
}

.column {
    border: 2px solid black;
    padding: 2em;
    flex: 1;
}
</style>