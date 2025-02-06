<script>
// let id = 0;

// export default {
//   data() {
//     return {
//       newTodo: "",
//       todos: [
//         { id: id++, text: "Вивчити HTML" },
//         { id: id++, text: "Вивчити JavaScript" },
//         { id: id++, text: "Вивчити Vue" },
//       ],
//     };
//   },
//   methods: {
//     addTodo() {
//       if (!this.newTodo.trim()) return;

//       this.todos.push({
//         id: id++,
//         text: this.newTodo,
//       });

//       this.newTodo = "";
//     },
//     removeTodo(todo) {
//       this.todos = this.todos.filter((item) => item.id !== todo.id);
//     },
//   },
// };
</script>

// --------Composition API-------------

<script setup>
import { ref } from "vue";

let id = 0;

const newTodo = ref("");
const todos = ref([
  { id: id++, text: "Вивчити HTML" },
  { id: id++, text: "Вивчити JavaScript" },
  { id: id++, text: "Вивчити Vue" },
]);

function addTodo() {
  if (!newTodo.value) return;

  todos.value.push({
    id: id++,
    text: newTodo.value,
  });

  newTodo.value = "";
}

function removeTodo(todo) {
  todos.value = todos.value.filter((item) => item.id !== todo.id);
}
</script>

<template>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo" />
    <button>Додати завдання</button>
  </form>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
</template>
