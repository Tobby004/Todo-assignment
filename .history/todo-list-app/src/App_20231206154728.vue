<template>
  <div id="app">
    <h1>Todo List</h1>
    <div class="input-container">
      <input v-model="newTodo" @keyup.enter="addTodo" placeholder="Add new todo" class="input-field">
      <button @click="addTodo" class="add-button">Add</button>
    </div>
    <ul>
      <li v-for="(todo, index) in todos" :key="index" class="todo-item">
        <span>{{ todo }}</span>
        <button @click="editTodo(index)" class="edit-button">Edit</button>
        <button @click="deleteTodo(index)" class="delete-button">Delete</button>
      </li>
    </ul>
  </div>
</template>



<script>
export default {
  data() {
    return {
      todos: [],
      newTodo: '',
      editedTodoIndex: null,
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        if (this.editedTodoIndex !== null) {
          this.todos[this.editedTodoIndex] = this.newTodo;
          this.newTodo = '';
          this.editedTodoIndex = null;
        } else {
          this.todos.push(this.newTodo);
          this.newTodo = '';
        }
      }
    },
    editTodo(index) {
      this.newTodo = this.todos[index];
      this.editedTodoIndex = index;
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    },
  },
};
</script>

<style scoped>
/* Dark-themed styles */
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background-color: #222;
  color: #eee;
}

#app {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #333; /* Darker background for the app container */
  border-radius: 8px; /* Rounded corners */
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3); /* Subtle shadow effect */
}

h1 {
  text-align: center;
}

.input-field {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  background-color: #444; /* Input field background */
  color: #eee; /* Input field text color */
}

.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  margin-bottom: 8px;
  background-color: #555; /* Todo item background */
  border-radius: 5px;
  transition: background-color 0.3s ease;
}

.todo-item:hover {
  background-color: #666; /* Darken todo item on hover */
}

.edit-button,
.delete-button {
  padding: 5px 10px;
  border: none;
  border-radius: 3px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.edit-button:hover {
  background-color: #3a7bd5;
}

.delete-button:hover {
  background-color: #d9534f;
}
</style>
