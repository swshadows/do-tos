<template>
  <router-link :to="{ name: 'todo', params: { id: todo.id } }">
    <h1>
      <span v-if="todo.completed">✅</span>
      <span v-else>❌</span>
      {{ reducedTitle }}
    </h1>
  </router-link>
  <div class="options">
    <button v-if="!todo.completed" @click="handleDone(todo.id)" class="done">✔ Marcar como concluido</button>
    <button v-else @click="handleDone(todo.id)" class="pending">✖ Marcar como Pendente</button>
    <button @click="handleDelete(todo.id)" class="delete">🗑</button>
  </div>
</template>

<script>
import { computed } from "@vue/runtime-core";
export default {
  props: ["todo"],
  emits: ["updateLS"],
  setup(props, { emit }) {
    const handleDelete = (id) => {
      const toDos = JSON.parse(localStorage.toDos);
      const filterTodos = toDos.filter((item) => item.id != id);
      filterTodos.map((item, index) => (item.id = index));
      localStorage.toDos = JSON.stringify(filterTodos);
      emit("updateLS");
    };

    const handleDone = (id) => {
      const toDos = JSON.parse(localStorage.toDos);
      toDos.map((item) => {
        if (item.id == id) item.completed = !item.completed;
      });
      localStorage.toDos = JSON.stringify(toDos);
      emit("updateLS");
    };

    const reducedTitle = computed(() => {
      if (props.todo.title.length > 20) return props.todo.title.slice(0, 20) + "...";
      return props.todo.title;
    });
    return { reducedTitle, handleDone, handleDelete };
  },
};
</script>

<style scoped>
h1 {
  margin: 0;
  font-size: 1.4rem;
}
a {
  display: inline-block;
  color: #9c6ebb;
  text-decoration: none;
}
a:hover {
  text-decoration: underline;
}
.options {
  display: flex;
  gap: 10px;
}
.options button {
  border: 1px solid transparent;
  padding: 5px;
  cursor: pointer;
  color: #fff;
  transition: 0.1s all;
}
button:hover {
  transform: scale(1.1);
}
button.done {
  background: #258570;
}
button.pending {
  background: #b6921c;
}
button.delete {
  background: #ff4646;
}
</style>
