<script>
  import axios from "axios";
  import TasksIndex from "./TasksIndex.vue";
  import TasksNew from "./TasksNew.vue";
  import Modal from "./Modal.vue";

  export default {
    components: {
      TasksIndex,
      TasksNew,
      Modal
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
      handleCreateTask: function (params) {
        console.log("params", params);
        axios.post("http://localhost:5000/tasks.json", params).then(response => {
          console.log("tasks create", response);
          this.tasks.push(response.data);
        })
        .catch((error) => {
          console.log("tasks create error", error.repsonse);
        });
      }
    },
  };
</script>

<template>
  <main>
    <TasksNew v-on:createTask="handleCreateTask"/>
    <TasksIndex v-bind:tasks="tasks"/>
    <Modal v-bind:show="true">
      <h1>Test</h1>
    </Modal>
  </main>
</template>

<style></style>