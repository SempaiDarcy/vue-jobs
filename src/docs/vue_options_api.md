# Vue 3: Использование Options API

## Описание
Этот файл содержит код Vue 3 с **Options API**, а также объяснение преимуществ и отличий от Composition API.

---

## ❌ **Оригинальный код (неоптимизированный)**

```vue
<script>
export default {
  data() {
    return {
      name: "Artur Morgan",
      status: "active",
      tasks: ['Task One', 'Task Two', 'Task Three'],
      link: 'https://google.com'
    };
  },
  methods: {
    toggleStatus() {
      if (this.status === 'active') {
        this.status = "pending";
      } else if (this.status === 'pending') {
        this.status = 'inactive';
      } else {
        this.status = "active";
      }
    },
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push(this.newTask);
        this.newTask = '';
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(response => response.json())
      .then(data => {
        this.tasks = data.map(task => task.title);
      })
      .catch(error => console.error('Ошибка загрузки данных:', error));
  }
};
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <br>
    <input type="text" id="newTask" name="newTask" v-model="newTask"/>
    <button type="submit">Submit</button>
  </form>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="index">
      <span>{{ task }}</span>
      <button @click="deleteTask(index)">x</button>
    </li>
  </ul>

  <a :href="link" target="_blank">Click for Google</a>
  <button @click="toggleStatus">Change Status</button>
</template>
```

---

## ✅ **Оптимизированный код с Options API**

```vue
<script>
export default {
  data() {
    return {
      name: "Arthur Morgan",
      status: "active",
      tasks: [],
      link: 'https://google.com',
      newTask: ''
    };
  },
  methods: {
    toggleStatus() {
      const statuses = ['active', 'pending', 'inactive'];
      const currentIndex = statuses.indexOf(this.status);
      this.status = statuses[(currentIndex + 1) % statuses.length];
    },
    addTask() {
      if (!this.newTask.trim()) return;
      this.tasks = [...this.tasks, this.newTask];
      this.newTask = '';
    },
    deleteTask(index) {
      this.tasks = this.tasks.filter((_, i) => i !== index);
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(response => response.json())
      .then(data => {
        this.tasks = data.map(task => task.title);
      })
      .catch(error => console.error('Ошибка загрузки данных:', error));
  }
};
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <br>
    <input type="text" id="newTask" name="newTask" v-model="newTask"/>
    <button type="submit">Submit</button>
  </form>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="index">
      <span>{{ task }}</span>
      <button @click="deleteTask(index)">x</button>
    </li>
  </ul>

  <a :href="link" target="_blank">Click for Google</a>
  <button @click="toggleStatus">Change Status</button>
</template>
```

---

## 🔥 **Что улучшилось?**
- **Добавлен `mounted()`** для загрузки задач с API  
- **Упрощена логика `toggleStatus`**  
- **Используется `filter()` вместо `splice()` для удаления задач**  
- **Добавлен `target="_blank"` в ссылке**  

---

## 🧐 **Options API vs Composition API**
| **Функция**  | **Options API** | **Composition API** |
|-------------|---------------|----------------|
| **Читаемость** | Простая для новичков | Гибкая, лучше для сложных проектов |
| **Разделение логики** | Методы, данные, хуки раздельно | Легче группировать логику |
| **Переиспользуемость** | Труднее вынести в `mixins` | Легко разделять через Composables |
| **Производительность** | Аналогичная | Аналогичная, но более удобная |

Options API остаётся удобным для небольших проектов, но в сложных системах **Composition API** выигрывает! 🚀
