<template>
  <Board :columns="columns"></Board>
</template>

<script>
import Board from './components/Board.vue';

export default {
  created() {
    const saved = localStorage.getItem("kanban-board");
    if (saved) {
      this.columns = JSON.parse(saved);
    }
  },
  watch: {
    columns: {
      deep: true,
      handler(newColumns) {
        localStorage.setItem("kanban-board", JSON.stringify(newColumns));
      }
    }
  },
  components: { Board },
  data() {
    return {
      columns: [
        { col_id: 1, name: "To Do", tasks: [{ task_id: 1, task_text: "First Task to do" }] },
        { col_id: 2, name: "In Progress", tasks: [{ task_id: 2, task_text: "First Task In Progress" }] },
        { col_id: 3, name: "Done", tasks: [{ task_id: 3, task_text: "Done Task" }, { task_id: 4, task_text: "Done Task" }] }
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