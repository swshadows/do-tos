<template>
  <div class="home">
    <div class="to-dos">
      <FilterButtons @filter="filterUpdate" />
      <ToDos :filter="filter" />
    </div>
  </div>
</template>

<script>
import ToDos from "@/components/ToDos.vue";
import FilterButtons from "@/components/FilterButtons.vue";
import { ref } from "@vue/reactivity";
export default {
  name: "HomeView",
  components: { ToDos, FilterButtons },
  setup() {
    if (!localStorage.toDos) localStorage.setItem("toDos", "[]");
    const filter = ref("todos");

    const filterUpdate = (f) => {
      filter.value = f;
    };

    return { filterUpdate, filter };
  },
};
</script>

<style scoped>
.to-dos {
  padding: 10px;
}
</style>
