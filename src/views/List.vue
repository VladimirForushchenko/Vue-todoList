<template>
  <div>
    <h1>List</h1>
    <div class="row">
      <div class="input-field s4 col">
      <select ref="select" v-model="filter">
      <option value="" disabled selected>Choose your option</option>
      <option value="active">Active</option>
      <option value="outdated">Outdated</option>
      <option value="completed">Completed</option>
    </select>
    <label>Status filter</label>
    </div>
    </div>

    <button v-if="filter" @click="filter = null" class="btn btn-small red">Clear filter</button>
    <hr>

    <table v-if="tasks.length" class="highlight">
      <thead>
        <tr>
          <th>#</th>
          <th>Tittle</th>
          <th>Date</th>
          <th>Description</th>
          <th>Status</th>
          <th>Open</th>
          <th>Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, idx) of displayTasks"
        :key="task.id"
        >
      <td>{{ idx + 1 }}</td>
      <td>{{ task.title }}</td>
      <td>{{ new Date(task.date).toLocaleDateString() }}</td>
      <td class="length-td"><div class="text">{{ task.description }}</div></td>
      <td>{{ task.status }}</td>
      <td>
        <router-link :to="'/task/' + task.id" tag="button" class="btn btn-small">
          Open
        </router-link>
      </td>
      <td>
        <button type="button" @click="deleteTask" class="btn btn-small red">Del</button>
      </td>
    </tr>
      </tbody>
    </table>
    <p v-else>No tasks</p>
  </div>
</template>

<script>

export default {
  data: () => ({
    filter: null,
  }),
    computed: {
        tasks() {
            return this.$store.getters.tasks
        },
        displayTasks() {
          return this.tasks.filter(t => {
            if (!this.filter) {
              return true
            }
            return t.status === this.filter
          })
        }
    },
    mounted() {
      M.FormSelect.init(this.$refs.select)
    },
    methods: {
      deleteTask() {
      this.$store.dispatch('deleteTask', this.task.id)
      } 
    }
}
</script>

<style lang="scss" scoped>

.text {
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow: hidden;
}
.length-td {
  max-width: 300px;
}
</style>
