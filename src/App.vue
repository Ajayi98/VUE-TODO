
<template>
  <div id="app">
    <div class="app-wrapper">
      <h1>Vue Todo App</h1>
      <form @submit.prevent="addTodo">
              <input v-model="newTodo" placeholder="Enter a new todo" />
        <button type="submit">Add Todo</button>
      </form>
    </div>
    <div>
      <ul>
        <TodoList :todos="todos" @edit="editTodo" @delete="deleteTodo" />
      </ul>
    </div>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue';

export default {
  components: {
    TodoList,
  },
  data() {
    return {
      newTodo: '',
      todos: [],
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() === '') return;
      const newTodo = {
        id: Date.now(),
        text: this.newTodo.trim(),
      };
      this.todos.push(newTodo);
      this.newTodo = '';
    },
    editTodo(editedTodo) {
      const index = this.todos.findIndex(todo => todo.id === editedTodo.id);
      if (index !== -1) {
        this.todos[index].text = editedTodo.text;
      }
    },
    deleteTodo(todoId) {
      this.todos = this.todos.filter(todo => todo.id !== todoId);
    },
  },
};
</script>

<style>
#app {
  text-align: center;
  margin-top: 100px;
}

form {
  margin-bottom: none;
}

input {
  padding: 8px;
  margin-right: 8px;
  margin-top: 25px;
}

button {
  padding: 8px;
  margin-left: 23px;
}
ul {
  list-style: disc;
  padding: 0;
}
h1{
  color: #3f51b5;
}

.app-wrapper{
  margin-top: -40px;

  /* border: 1px solid #3f51b5; */
  padding: 2px;
  /* border-radius: 2px; */
  /* box-shadow: 0 0 10px #3f51b5; */
}





</style>
