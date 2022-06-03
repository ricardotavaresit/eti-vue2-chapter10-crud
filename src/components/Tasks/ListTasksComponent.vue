<template>
  <div>
    <h2>{{ title }}</h2>

    <form class="form form-inline" v-on:submit.prevent="save">
      <input type="text" placeholder="Task name" v-model="task.name" />
      <button type="submit" class="btn btn-primary">Send</button>
    </form>

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
      task: {
        id: "",
        name: "",
      },
    };
  },
  methods: {
    save() {
      this.tasks.push({
        id: this.tasks.length + 1,
        name: this.task.name,
      });
      this.task = {
        id: "",
        name: "",
      };
    },
  },
};
</script>

<style scoped>
.actions {
  width: 150px;
}

form {
  margin: 20px 0;
}
</style>
