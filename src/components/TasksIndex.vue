<script>
export default {
  props: {
    tasks: Array,
  },
};
</script>

<template>
  <div>
    <h1>All tasks</h1>
    <div v-for="task in tasks" v-bind:key="task.id">
      <h2>{{  task.name }}</h2>
      <p>estimated time: {{ task.estimated_time }}</p>
      <p>deadline: {{ task.deadline }}</p>
      <button v-on:click="$emit('showTask', task)">More info</button>
      <hr>
    </div>
  </div>
  <br>
</template>

<style></style>