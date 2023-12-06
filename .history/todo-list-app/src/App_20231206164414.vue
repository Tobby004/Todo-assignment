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
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
}

h1 {
  text-align: center;
}

.input-container {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.input-field {
  width: 200px; /* Reducing input width */
  padding: 10px;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  background-color: #444;
  color: #eee;
}

.add-button {
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  background-color: #3a7bd5;
  color: #fff;
  transition: background-color 0.3s ease;
}

.add-button:hover {
  background-color: #2e5aa3;
}
.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  margin-bottom: 8px;
  background-color: #555;
  border-radius: 5px;
  transition: background-color 0.3s ease;
}

.todo-item:hover {
  background-color: #666;
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
