<template>
  <div id="app">
    <list-tasks-component />
  </div>
</template>

<script>
import ListTasksComponent from "./components/Tasks/ListTasksComponent";
export default {
  name: "app",
  data() {
    return {
      msg: "Welcome to Your Vue.js App",
    };
  },
  components: {
    ListTasksComponent,
  },
};
</script>
