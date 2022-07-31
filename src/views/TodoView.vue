<template>
  <div v-if="thisTodo[0]">
    <h1>{{ thisTodo[0].title }}</h1>
    <p>{{ thisTodo[0].body }}</p>
  </div>
  <div v-else>Todo não encontrada</div>
</template>

<script>
import { computed } from "@vue/runtime-core";
export default {
  props: ["id"],
  setup(props) {
    const data = JSON.parse(localStorage.toDos);

    const thisTodo = computed(() => {
      return data.filter((item) => item.id == props.id);
    });

    return { thisTodo };
  },
};
</script>

<style></style>
