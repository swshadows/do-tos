<template>
  <div class="home">
    <h1>✅ Do-Tos</h1>
    <p>🎈 Uma lista de tarefas carismática</p>
    <div class="to-dos">
      <ToDos :todos="toDos" />
    </div>
    <AddTodo @updateLS="update" />
  </div>
</template>

<script>
import AddTodo from "@/components/AddTodo.vue";
import ToDos from "@/components/ToDos.vue";
import { ref } from "@vue/reactivity";
export default {
  name: "HomeView",
  components: { AddTodo, ToDos },
  setup() {
    if (!localStorage.toDos) localStorage.setItem("toDos", "[]");
    const toDos = ref(JSON.parse(localStorage.toDos));
    const update = (newTodos) => {
      toDos.value = newTodos;
    };
    return { update, toDos };
  },
};
</script>

<style scoped>
.to-dos {
  padding: 10px;
}
</style>
