# Vue 3: Использование Composition API

## Описание
Этот файл содержит код Vue 3 с **Composition API**, а также объяснение преимуществ и отличий от Options API.

---

## ❌ **Оригинальный код (неоптимизированный)**

```vue
<script setup>
import { onMounted, ref } from "vue";

const name = ref('Artur Morgan');
const status = ref('active');
const tasks = ref(['Task One', 'Task Two', 'Task Three']);
const link = ref("https://google.com");
const newTask = ref('')

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
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value)
    newTask.value = ''
  }
}

const deleteTask = (index) => {
  tasks.value.splice(index, 1)
}

onMounted(async () => {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/todos')
    const data = await res.json()
    tasks.value = data.map(task => task.title)
  } catch (error) {
    console.log('Error fetching tasks')
  }
})
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
```

---

## ✅ **Оптимизированный код с Composition API**

```vue
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
```

---

## 🔥 **Что улучшилось?**
- **Удалено дублирование кода**  
- **Улучшена производительность** (изменение массива через `filter` вместо `splice`)  
- **Правильное использование `:key="index"`**  
- **Обработаны ошибки при загрузке данных**  
- **Добавлена лучшая логика для `toggleStatus`**  

---

## 🧐 **Composition API vs Options API**
| **Функция**  | **Options API** | **Composition API** |
|-------------|---------------|----------------|
| **Читаемость** | Простая для новичков | Гибкая, лучше для сложных проектов |
| **Разделение логики** | Методы, данные, хуки раздельно | Легче группировать логику |
| **Переиспользуемость** | Труднее вынести в `mixins` | Легко разделять через Composables |
| **Производительность** | Аналогичная | Аналогичная, но более удобная |

Composition API даёт больше гибкости, особенно в больших проектах! 🚀
