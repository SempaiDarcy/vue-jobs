<script setup>
import { onMounted, ref } from "vue";

const name = ref('Arthur Morgan');
const status = ref('active');
const tasks = ref([]);
const link = ref("https://google.com");
const newTask = ref('');

const toggleStatus = () => {
  const statuses = ['active', 'pending', 'inactive'];
  status.value = statuses[(statuses.indexOf(status.value) + 1) % statuses.length];
};

const addTask = () => {
  if (!newTask.value.trim()) return;
  tasks.value = [...tasks.value, newTask.value];
  newTask.value = '';
};

const deleteTask = (index) => {
  tasks.value = tasks.value.filter((_, i) => i !== index);
};

onMounted(async () => {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/todos?_limit=5');
    const data = await res.json();
    tasks.value = data.map(task => task.title);
  } catch (error) {
    console.error('Ошибка загрузки данных:', error);
  }
});
</script>
<template>
  <h1>{{ name }}</h1>
  <p v-if="status==='active'">User is active</p>
  <p v-else-if="status==='pending'">User is pending</p>
  <p v-else>User is inactive</p>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <br>
    <input type="text" id="newTask" name="newTask" v-model="newTask"/>
    <button type="submit" @click="addTask">Submit</button>
  </form>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task,index) in tasks" :key="task">
      <span @key="index">
        {{ task }}
      </span>
      <button @click="deleteTask(index)">
        x
      </button>
    </li>
  </ul>
  <!--  <a v-bind:href="link">Click for Google</a>-->
  <a :href="link">Click for Google</a>

  <!--  <button v-on:click="toggleStatus">Change Status</button>-->
  <button @click="toggleStatus">Change Status</button>
</template>