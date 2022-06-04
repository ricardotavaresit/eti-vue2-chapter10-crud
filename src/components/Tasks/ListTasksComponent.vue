<template>
  <div>
    <h2>{{ title }}</h2>

    <div class="row">
      <div class="col">
        <form class="form form-inline" v-on:submit.prevent="onSubmit">
          <input type="text" placeholder="Search" v-model="filter" />
        </form>
      </div>
      <div class="col">
        <form class="form form-inline" v-on:submit.prevent="onSubmit">
          <input type="text" placeholder="Task name" v-model="task.name" />
          <button type="submit" class="btn btn-primary">Send</button>
        </form>
      </div>
    </div>
    <table class="table">
      <thead>
        <tr>
          <th>Id</th>
          <th>Name</th>
          <th class="actions">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-bind:key="index" v-for="(task, index) in filteredItems">
          <td>{{ task.id }}</td>
          <td>{{ task.name }}</td>
          <td>
            <a class="btn btn-primary" href="" v-on:click.prevent="edit(index)"
              >Edit</a
            >
            <a
              class="btn btn-danger"
              href=""
              v-on:click.prevent="destroy(index)"
              >Delete</a
            >
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
      filter: "",
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
    destroy(index) {
      this.tasks.splice(index);
    },
  },
  computed: {
    filteredItems() {
      if (!this.filter) {
        return this.tasks;
      }

      /*** Version 1
      return this.tasks.filter((task) => {
        return task.name.indexOf(this.filter) > -1;
      });
      */

      /*** Version 2
      return this.tasks.filter((task) => {
        return task["name"].toLowerCase().includes(this.filter.toLowerCase());
      });
      */

      /* Version 3*/
      return this.tasks.filter(
        (task) =>
          task.name.toLowerCase().indexOf(this.filter.toLowerCase()) > -1
      );
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
