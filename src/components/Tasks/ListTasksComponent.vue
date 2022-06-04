<template>
  <div>
    <h2>{{ title }}</h2>

    <form class="form form-inline" v-on:submit.prevent="onSubmit">
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
            <a class="btn btn-primary" href="" v-on:click.prevent="edit(index)"
              >Edit</a
            >
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
      updating: false,
      updatedIndex: "",
    };
  },
  methods: {
    onSubmit() {
      if (this.updating) {
        this.update();
        return;
      }
      this.save();
    },
    save() {
      this.tasks.push({
        id: this.tasks.length + 1,
        name: this.task.name,
      });
      this.clearForm();
    },
    edit(index) {
      this.task = this.tasks[index];
      this.updatedIndex = index;
      this.updating = true;
    },
    update() {
      this.tasks[this.updatedIndex] = this.task;
      this.updating = false;
      this.clearForm();
    },
    clearForm() {
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
