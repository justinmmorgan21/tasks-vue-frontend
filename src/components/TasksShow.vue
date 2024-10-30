<script>
export default {
  props: {
    task: Object,
  },
  data: function () {
    return {
      editTaskParams: {},
    };
  },
  created: function () {
    this.editTaskParams = { ...this.task };
  },
  methods: {
    handleSubmit: function () {
      this.$emit("updateTask", this.task.id, this.editTaskParams);
    },
  },
};
</script>

<template>
  <div>
    <h1>Task information</h1>
    <p>Name: {{ task.name }}</p>
    <p>Estimated Time: {{ task.estimated_time }}</p>
    <p>Deadline: {{ task.deadline }}</p>
    <form v-on:submit.prevent="handleSubmit">
      <div>
        Name:
        <input v-model="editTaskParams.name" type="text">
      </div>
      <div>
        Estimated Time:
        <input v-model="editTaskParams.estimated_time" type="text">
      </div>
      <div>
        Deadline:
        <input v-model="editTaskParams.deadline" type="text">
      </div>
      <button type="submit">Update task</button>
    </form>
    <button v-on:click="$emit('destroyTask', task)">Destroy task</button>
  </div>
</template>

<style></style>