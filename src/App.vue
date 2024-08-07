<template>
  <div class="divprincipale">
    <h1>Vue 3 Todo APP</h1>
    <form @submit.prevent="addNewTodo">
      <label for="newTodo">New Todo</label>
      <input v-model="newTodo" name="newTodo" id="newTodo" placeholder="Add a new task...">
      <button>Add Todo</button>
    </form>
    <button @click="removeAllTodos">Remove All</button>
    <button @click="markAllDone">Mark All Done</button>
    <ul>
      <li v-for="(todo, index) in todos" :key="todo.id" class="todo">
        <h3 :class="{done: todo.done}" @click="toggleDone(todo)">{{ todo.content }}</h3>
       
      </li>
    </ul>
    <button @click="removeTodo(index)">Remove</button>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const newTodo = ref('');
    const todos = ref([]);

    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = '';
    }

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    function markAllDone() {
      todos.value.forEach((todo) => todo.done = true);
    }

    function removeAllTodos() {
      todos.value = [];
    }

    return {
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAllDone,
      removeAllTodos,
    };
  },
};
</script>

<style scoped>
body {
  font-family: 'Arial', sans-serif;
  background-color: #f5f5f5;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.divprincipale {
  background-color: #ffffff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  max-width: 500px;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

h1 {
  font-size: 24px;
  color: #333;
  text-align: center;
  margin-bottom: 20px;
}

form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 20px;
  width: 100%;
}

input {
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ddd;
  border-radius: 4px;
  width: 100%;
}

input:focus {
  border-color: #007bff;
  outline: none;
}

button {
  background-color:#007bff; /* couleur saumon */
  color: white;
  border: none;
  padding: 10px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  width: 100%;
  margin-bottom: 10px;
}

button:hover {
  background-color: #ff6f47; /* couleur saumon plus foncée pour hover */
}

ul {
  list-style: none;
  padding: 0;
  width: 100%;
}

.todo {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #eee;
}

.todo h3 {
  margin: 0;
  font-size: 18px;
  color: #333;
  cursor: pointer;
}

.todo h3.done {
  text-decoration: line-through;
  color: #aaa;
}

.todo button {
  background-color: #5f71c0;
  color: white;
  border: none;
  padding: 10px 50px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
  display:' block';
}

.todo button:hover {
  background-color: #5f77b9;
}
</style>
