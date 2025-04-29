<template>
    <div class="task">
        <p>{{ task.task_text }}</p>
    </div>
</template>

<script>
export default {
    props: ['task'],

}
</script>

<style scoped>
.task {
    border: 2px solid black;
    padding: 1em;
}
</style>
