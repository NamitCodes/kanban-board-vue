<template>
    <div class="task" draggable="true" @dragstart="handleDragStart">
        <p>{{ task.task_text }}</p>
    </div>
</template>

<script>
export default {
    props: ['task', 'columnId'],
    methods: {
        handleDragStart(event) {
            const payload = {
                taskId: this.task.task_id,
                columnId: this.columnId
            };
            event.dataTransfer.setData("application/json", JSON.stringify(payload))
            console.log(payload)
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
    border-left: 4px solid #42b983;
    /* Vue green for flair */
    padding: 1em;

    display: flex;
}
</style>
