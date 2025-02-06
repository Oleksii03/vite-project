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
  <div class="box">
    <div>
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
    </div>
  </div>
</template>

<style lang="scss">
@import "./assets/styles/main";

.box {
  height: 100vh;
  display: grid;
  place-content: center;

  & > div {
    border: 4px solid #18191a;
    border-radius: 10px;
    padding: 30px;
    background-color: #d7cbcb;
    & > form {
      display: flex;
      flex-direction: column;
      row-gap: 10px;
      border-bottom: 2px dashed #000;
      padding-bottom: 10px;

      & > input {
        font-size: inherit;
        border-radius: 5px;
      }
      & > button {
        padding: 5px 10px;
        border-radius: 5px;
        background-color: #007bff;
        color: #fff;
        cursor: pointer;
        font-size: inherit;
      }
    }
  }
}
</style>
