
<template>
    <div>
      <Todo v-for="todo in todos" :key="todo.id" :todo="todo" @edit="editTodo" @delete="deleteTodo" />
    </div>
  </template>
  
  <script>
    import Todo from './Todo.vue';
  
  export default {
    components: {
      Todo,

    },
    props: ['todos'],
    methods: {
      editTodo(todo) {
        this.$emit('edit', todo);
      },
      deleteTodo(todoId) {
        this.$emit('delete', todoId);
      }
    }
  };
  </script>
  