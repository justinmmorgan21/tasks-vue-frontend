<script>
  import axios from "axios";
  import TasksIndex from "./TasksIndex.vue";

  export default {
    components: {
      TasksIndex,
    },
    data: function() {
      return {
        tasks: [],
        // tasks: [
        //   { id: 1, name: "First", estimated_time: 120, deadline: "2024-11-01" },
        //   { id: 2, name: "Second", estimated_time: 90, deadline: "2024-11-02" }
        // ],
      };
    },
    created: function () {
      this.handleIndexTasks();
    },
    methods: {
      handleIndexTasks: function () {
        axios.get("http://localhost:5000/tasks.json").then(response => {
          console.log("tasks index", response);
          this.tasks = response.data;
        });
      },
    },
  };
</script>

<template>
  <main>
    <TasksIndex v-bind:tasks="tasks"/>
  </main>
</template>

<style></style>