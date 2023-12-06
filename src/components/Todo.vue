
<template>
  <div class="todo-item">
    <span v-if="!editing" @click="toggleEdit">{{ todo.text }}</span>
    <input v-if="editing" v-model="editedText" @blur="saveEdit" @keyup.enter="saveEdit" />
    <div class="edit-btn">
      <button v-if="!editing" @click="toggleEdit">Edit</button>
      <button @click="deleteTodo">Delete</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['todo'],
  data() {
    return {
      editing: false,
      editedText: this.todo.text,
    };
  },
  methods: {
    toggleEdit() {
      this.editing = !this.editing;
    },
    saveEdit() {
      this.$emit('edit', { id: this.todo.id, text: this.editedText });
      this.editing = false;
    },
    deleteTodo() {
      this.$emit('delete', this.todo.id);
    },
  },
};
</script>

<style scoped>
.todo-item {
  margin: 8px 0;
  border-bottom: none;
  padding-bottom: 4px;
  cursor: pointer;
}

/* .todo-item span {
  user-select: none;
} */

.todo-item input {
  width: 15%;
  padding: 4px;
}
.todo-item button {
  margin-left: 8px;
  padding: 4px;
}
</style>
