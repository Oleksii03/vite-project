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
import { onMounted, onUnmounted, ref } from "vue";
const id = ref(0);

function change() {
  id.value++;
  console.log(id.value);
}

onMounted(() => {
  id.value = 10;
});

onUnmounted(() => {
  id.value = 20;
});
</script>

<template>
  <div>{{ id }}</div>
  <button @click="change">X</button>
</template>
