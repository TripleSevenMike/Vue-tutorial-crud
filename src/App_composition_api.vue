<!-- <script>
// composition api

import {ref} from 'vue'

export default {
  setup (){
    const name = ref('John Doe')
    const status = ref('active')
    const tasks = ref([
      { id: 1, title: 'Task 1', completed: false },
      { id: 2, title: 'Task 2', completed: true },
      { id: 3, title: 'Task 3', completed: false },
    ])
    const link = 'https://vuejs.org'

    const toggleStatus = () => {
      status.value = status.value === 'active' ? 'inactive' : 'active'
    }

    return {
      name,
      status,
      tasks,
      link,
      toggleStatus,
    }
  }
}
</script> -->

<script setup>
// composition api

import {ref, onMounted} from 'vue'

    const name = ref('John Doe')
    const status = ref('active')
    const tasks = ref([
      { id: 1, title: 'Task 1', completed: false },
      { id: 2, title: 'Task 2', completed: true },
      { id: 3, title: 'Task 3', completed: false },
    ])
    const newTask = ref('')
    const link = 'https://vuejs.org'

    const toggleStatus = () => {
      status.value = status.value === 'active' ? 'inactive' : 'active'
    }

    const addTask = () => {
      if (newTask.value.trim() !== '') {
        tasks.value.push({
          id: tasks.value.length + 1,
          title: newTask.value,
          completed: false,
        })
        newTask.value = ''
      }
    }

    const deleteTask = (index) => {
      tasks.value.splice(index,1)
    }

    onMounted(async ()=>{
      try{
        const response = await fetch('https://jsonplaceholder.typicode.com/todos')
        const data = await response.json();
        console.log(data)
        data.map((item) => {
          tasks.value.push({
            id: item.id,
            title: item.title,
            completed: item.completed,
          })
        })
     
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    });

</script>


<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is Inactive</p>


  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="New Task" v-model="newTask"/>
  <button type="submit">Submit</button>
  </form>



  <h3>Tasks</h3>
  <ul>
    <li v-for="(task,index) in tasks" :key="task.id">
      <span v-if="task.completed">✔️</span>
      <span v-else>❌</span>
      <span>{{ task.title }}</span>
      <button @click="deleteTask(index)">
x
      </button>
    </li>
  </ul>

  <a v-bind:href="link">Vue.js Documentation</a>
  <a :href="link">Vue.js Documentation</a>

  <!-- <button v-on:click="toggleStatus">Change status</button> -->
  <button @click="toggleStatus">Change status</button>
</template>
