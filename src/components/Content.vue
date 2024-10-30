<script>
  import axios from "axios";
  import TasksIndex from "./TasksIndex.vue";
  import TasksNew from "./TasksNew.vue";
  import TasksShow from "./TasksShow.vue"
  import Modal from "./Modal.vue";

  axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';

  export default {
    components: {
      TasksIndex,
      TasksNew,
      TasksShow,
      Modal
    },
    data: function() {
      return {
        tasks: [],
        currentTask: {},
        isTaskShowVisible: false,
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
        console.log("params sent to backend:", params);
        axios.post("http://localhost:5000/tasks.json", params).then(response => {
          console.log("tasks create", response);
          this.tasks.push(response.data);
        })
        .catch((error) => {
          console.log("tasks create error", error.repsonse);
        });
      },
      handleShowTask: function (task) {
        console.log("handleShowTask", task);
        this.currentTask = task;
        this.isTaskShowVisible = true;
      },
      // FIX THIS UPDATE ACTION LATER - not passing params properly?
      handleUpdateTask: function (id, params) {
      console.log("handleUpdateTask", id, params);
      axios
        .patch(`http://localhost:5000/tasks/${id}.json`, params)
        .then((response) => {
          console.log("tasks update", response);
          this.tasks = this.tasks.map((task) => {
            if (task.id === response.data.id) {
              return response.data;
            } else {
              return task;
            }
          });
          console.log("CLOSING");
          this.handleClose();
        })
        .catch((error) => {
          console.log("tasks update error", error.response);
        });
      },
      handleDestroyTask: function (task) {
        axios.delete(`http://localhost:5000/tasks/${task.id}.json`).then(response => {
          console.log("tasks destroy", response);
          var index = this.tasks.indexOf(task);
          this.tasks.splice(index, 1);
          this.handleClose();
        });
      },
      handleClose: function () {
        this.isTaskShowVisible = false;
      }
    },
  };
</script>

<template>
  <main>
    <TasksNew v-on:createTask="handleCreateTask"/>
    <TasksIndex v-bind:tasks="tasks" v-on:showTask="handleShowTask"/>
    <Modal v-bind:show="isTaskShowVisible" v-on:close="handleClose">
      <TasksShow v-bind:task="currentTask" v-on:updateTask="handleUpdateTask" v-on:destroyTask="handleDestroyTask"/>
    </Modal>
  </main>
</template>

<style></style>