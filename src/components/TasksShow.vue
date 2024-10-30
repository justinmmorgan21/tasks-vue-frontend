<script>
export default {
  props: {
    task: Object,
  },
};
</script>

<template>
  <div>
    <h1>Task information</h1>
    <p>Name: {{ task.name }}</p>
    <p>Estimated Time: {{ task.estimated_time }}</p>
    <p>Deadline: {{ task.deadline }}</p>
  </div>
</template>

<style></style>