<script>
export default {
  data() {
    return {
      name: 'Malu',
      status: 'active',
      tasks: ['study', 'cook', 'eat', 'clean'],
      colors: ['red', 'blue', 'green', 'blue'],
      link: 'https://google.com',
    }
  },
  methods: {
    toggleStatus() {
      if (this.status === 'active') {
        this.status = 'pending';
      } else if (this.status === 'pending') {
        this.status = 'inactive';
      } else {
        this.status = 'active';
      }
    }
  }
};
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>
  <h3>Tasks:</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>
  <h3>Color</h3>
  <ul>
    <li v-for="color in colors" :key="color">{{ color }}</li>
  </ul>
  <a :href="link">Go to google</a>
  <br>
  <button @click="toggleStatus">Change status</button>
</template>
