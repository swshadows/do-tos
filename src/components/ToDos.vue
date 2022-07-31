<template>
  <div class="card" v-for="todo in todos" :key="todo.id">
    <router-link :to="{ name: 'todo', params: { id: todo.id } }">
      <h1>{{ todo.title }}</h1>
    </router-link>

    <p>{{ todo.body }}</p>
  </div>
</template>

<script>
export default {
  props: ["todos"],
};
</script>

<style scoped>
.card {
  padding: 5px;
  border: 1px solid #eee;
}
h1,
p {
  margin: 0;
  font-size: 1rem;
}
a {
  color: #9c6ebb;
}
</style>
