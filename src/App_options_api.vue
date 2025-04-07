<script>
// options api
export default {
  data() {
    return {
      name: 'John Doe',
      status: 'pending',
      tasks: [
        { id: 1, title: 'Task 1', completed: false },
        { id: 2, title: 'Task 2', completed: true },
        { id: 3, title: 'Task 3', completed: false },
      ],
      link: 'https://vuejs.org',
    }
  },
  methods: {
    toggleStatus() {
      this.status = this.status === 'active' ? 'inactive' : 'active'
    },
  },
}
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is Inactive</p>

  <h3>Tasks</h3>
  <ul>
    <li v-for="task in tasks" :key="task.id">
      <span v-if="task.completed">✔️</span>
      <span v-else>❌</span>
      {{ task.title }}
    </li>
  </ul>

  <a v-bind:href="link">Vue.js Documentation</a>
  <a :href="link">Vue.js Documentation</a>

  <button v-on:click="toggleStatus">Change status</button>
  <button @click="toggleStatus">Change status</button>
</template>
