<template>
  <button class="filter-btn" :class="{ active: filter == 'all' }" @click="changeFilter('all')">Todos</button>
  <button class="filter-btn" :class="{ active: filter == 'pending' }" @click="changeFilter('pending')">Pendentes</button>
  <button class="filter-btn" :class="{ active: filter == 'completed' }" @click="changeFilter('completed')">Concluidos</button>
</template>

<script>
import { ref } from "@vue/reactivity";
export default {
  emits: ["filter"],
  setup(props, { emit }) {
    const filter = ref("all");

    const changeFilter = (fil) => {
      filter.value = fil;
      emit("filter", filter.value);
    };

    return { changeFilter, filter };
  },
};
</script>

<style>
.filter-btn {
  background: none;
  border: none;
  margin-bottom: 0.3rem;
  padding-right: 0.3rem;
  cursor: pointer;
}
.active {
  border-bottom: 4px solid #258570;
}
</style>
