<script setup>
import { ref, onMounted } from 'vue';

const name = ref('malu');
const status = ref('active');
const tasks = ref(['a', 'b', 'c']);
const newTask = ref('');

const toggleStatus = () => {
  if (status.value === 'active') {
    status.value = 'pending';
  } else if (status.value === 'pending') {
    status.value = 'inactive';
  } else {
    status.value = 'active';
  }
};

const addTask = () => {
  if (newTask.value) {
    tasks.value.push(newTask.value);
    newTask.value = '';
  }
}

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
}

onMounted(async () => {
  try {
    const res = await fetch('http://jsonplaceholder.typicode.com/todos');
    const data = await res.json();
    tasks.value = data.map((task) => task.title);
  } catch (error) {
    console.log('Error fetching tasks');
  }
})
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>

  <form @submit.prevent="addTask">
    <label for="newTask">New Task</label>
    <input type="text" name="newTask" id="newTask" v-model.trim="newTask">
    <button type="submit">Submit</button>
  </form>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>
        {{ task }}
        <button @click="deleteTask(index)">x</button>
      </span>
    </li>
  </ul>
  <br>
  <button @click="toggleStatus">Change status</button>
</template>
