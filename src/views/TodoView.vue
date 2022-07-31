<template>
  <div v-if="thisTodo[0]">
    <router-link :to="{ name: 'home' }">Voltar ao inicio</router-link>
    <h1>{{ thisTodo[0].title }}</h1>
    <p>
      <span>Status: </span>
      <span class="done" v-if="thisTodo[0].completed">✅ Concluido</span>
      <span class="not-done" v-else>❌ Não Concluido</span>
    </p>
    <p>Descrição: {{ thisTodo[0].body }}</p>
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

<style scoped>
.done,
.not-done {
  padding: 2px;
  color: white;
  border-radius: 5px;
}
.done {
  background: #28b85f;
}
.not-done {
  background: #bd361e;
}
h1,
p {
  word-wrap: break-word;
}
</style>
