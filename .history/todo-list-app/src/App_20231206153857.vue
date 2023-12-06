<template>
  <div id="app">
    <h1>Todo List</h1>
    <input v-model="newTodo" @keyup.enter="addTodo" placeholder="Add new todo">
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <span>{{ todo }}</span>
        <button @click="editTodo(index)">Edit</button>
        <button @click="deleteTodo(index)">Delete</button>
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
/* Add your CSS styles here */
</style>
