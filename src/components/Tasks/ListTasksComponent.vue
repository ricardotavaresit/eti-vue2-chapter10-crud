<template>
  <div>
    <h2>{{ title }}</h2>

    <table class="table">
      <thead>
        <tr>
          <th>Id</th>
          <th>Name</th>
          <th class="actions">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-bind:key="index" v-for="(task, index) in tasks">
          <td>{{ task.id }}</td>
          <td>{{ task.name }}</td>
          <td>
            <a class="btn btn-primary" href="">Edit</a>
            <a class="btn btn-danger" href="">Delete</a>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "Tasks List",
      tasks: [
        { id: 1, name: "Task 1" },
        { id: 2, name: "Task 2" },
        { id: 3, name: "Task 3" },
        { id: 4, name: "Task 4" },
        { id: 5, name: "Task 5" },
      ],
    };
  },
};
</script>

<style scoped>
.actions {
  width: 150px;
}
</style>
