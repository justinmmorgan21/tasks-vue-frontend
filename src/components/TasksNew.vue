<script>
export default {
  data: function () {
    return {
      newTaskParams: {},
    };
  },
  methods: {
    handleSubmit: function () {
      this.$emit("createTask", this.newTaskParams);
      this.newTaskParams = {};
    },
  },
};
</script>

<template>
  <div>
    <h1>New Task</h1>
    <form v-on:submit.prevent="handleSubmit">
      <div>
        Name:
        <input type="text" v-model="newTaskParams.name"/>
      </div>
      <div>
        Estimated Time:
        <input type="text" v-model="newTaskParams.estimated_time" />
      </div>
      <div>
        Deadline:
        <input type="text" v-model="newTaskParams.deadline" />
      </div>
      <button type="submit">Create task</button>
    </form>
  </div>
</template>

<style></style>