<script>
export default {
  data() {
    return {
      name: "Jhon Doe",
      status: 'inactive',
      tasks: ['task1', 'task2', 'task3'],
      link: "https://google.com"
    }
  },
  methods: {
    toggleStatus() {
      if (this.status === 'active') {
        console.log(` if || this status ==> ${(this.status)}`)
        this.status = 'pending'
      }
      else if (this.status === 'pending') {
        console.log(` else if || this status ==> ${(this.status)}`)
        this.status = 'inactive'
      }
      else {
        console.log(`else | this status ==> ${(this.status)}`)
        this.status = 'active'
      }
    }
  }
}
</script>

<template>
  <h1>Hello {{ name }}</h1>
  <p v-if="status === 'active'">
    User is active
  </p>
  <p v-else-if="status === 'inactive'"> User is inactive</p>
  <p v-else>User is Offline</p>
  <h3>tasks :</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>
  <a v-bind:href="link">Click for Google </a>
  <br>
  <button @click="toggleStatus">Change Status</button>
</template>


<style scoped>
h1 {
  color: red;
}
</style>


<script setup>
import { ref, onMounted } from 'vue'

const name = ref('Jhon Doe')
const status = ref('active')
const link = ref('https//google.com')
const tasks = ref(['Task One', 'Task Two', 'Task Three'])
const newTask = ref('')

const toggleStatus = () => {
  if (status.value === 'active') {
    status.value = 'pending'
  }
  else if (status.value === 'pending') {
    status.value = 'inactive'
  }
  else {
    status.value = 'active'
  }
}

const addTask = (taskName) => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value)
    newTask.value = ''
  }
}
const deleteTask = (index) => {
  tasks.value.splice(index, 1)
}

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos')
    const data = await response.json()
    console.log(data)
    tasks.value = data.map((task) => task.title
    )
  } catch {
    console.log("Error fetching data")
  }
})

</script>

<template>
  <h1>Hello {{ name }}</h1>
  <p v-if="status === 'active'">
    User is active
  </p>
  <p v-else-if="status === 'inactive'"> User is inactive</p>
  <p v-else>User is Offline</p>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask">
    <button type="submit">Submit</button>
  </form>


  <h3>tasks :</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>
        {{ task }}
      </span>
      <button @click="deleteTask(index)">X</button>
    </li>
  </ul>
  <a v-bind:href="link">Click for Google </a>
  <br>
  <button @click="toggleStatus">Change Status</button>
</template>


<style scoped>
h1 {
  color: red;
}
</style>