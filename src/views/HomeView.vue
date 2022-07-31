<template>
  <div class="home">
    <h1>✅ Do-Tos</h1>
    <p>🎈 Uma lista de tarefas carismática</p>
    <div class="to-dos">
      <FilterButtons @filter="filterUpdate" />
      <ToDos @updateLS="update" :filter="filter" :todos="toDos" />
    </div>
    <AddTodo @updateLS="update" />
  </div>
</template>

<script>
import AddTodo from "@/components/AddTodo.vue";
import ToDos from "@/components/ToDos.vue";
import FilterButtons from "@/components/FilterButtons.vue";
import { ref } from "@vue/reactivity";
export default {
  name: "HomeView",
  components: { AddTodo, ToDos, FilterButtons },
  setup() {
    if (!localStorage.toDos) localStorage.setItem("toDos", "[]");
    const toDos = ref(JSON.parse(localStorage.toDos));
    const filter = ref("todos");
    const update = () => {
      toDos.value = JSON.parse(localStorage.toDos);
    };

    const filterUpdate = (f) => {
      filter.value = f;
    };

    return { update, toDos, filterUpdate, filter };
  },
};
</script>

<style scoped>
.to-dos {
  padding: 10px;
}
</style>
