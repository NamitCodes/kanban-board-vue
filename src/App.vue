<template>
  <Board :columns="columns"></Board>
</template>

<script>
import Board from './components/Board.vue';

export default {
  components: { Board },
  data() {
    return {
      columns: [
        { col_id: 1, name: "To Do", tasks: [{ task_id: 1, task_text: "Start learning Vue JS" }] },
        { col_id: 2, name: "In Progress", tasks: [{ task_id: 2, task_text: "In Progress Ka Task" }] },
        { col_id: 3, name: "Done", tasks: [{ task_id: 3, task_text: "Done Ka Task" }, { task_id: 4, task_text: "Done Ka doosra Task" }] }
      ]
    }
  }
}
</script>

<style>
body {
  font-family: Arial, sans-serif;
  background-color: #f4f5f7;
  margin: 0;
  padding: 0;
}
</style>