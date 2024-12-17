<template>
    <div id="app">
      <h1>Управление задачами и очередями</h1>
      <QueueComponent />
      <TaskComponent />
    </div>
  </template>
  <script>
  import QueueComponent from './components/QueueComponent.vue';
  import TaskComponent from './components/TaskComponent.vue';
  export default {
 components: {
   QueueComponent,
  TaskComponent,
    },
  };
  </script>
  <style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    text-align: center;
  }
  </style>
  