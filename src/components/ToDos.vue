<template>
  <div class="card" v-for="todo in filteredTodos" :key="todo.id">
    <SingleTodo @updateLS="update" :todo="todo" />
  </div>
</template>

<script>
import SingleTodo from "@/components/SingleTodo.vue";
import { computed } from "@vue/runtime-core";
export default {
  props: ["todos", "filter"],
  emits: ["updateLS"],
  components: { SingleTodo },
  setup(props, { emit }) {
    const update = () => {
      emit("updateLS");
    };

    const filteredTodos = computed(() => {
      if (props.filter == "completed") return props.todos.filter((item) => item.completed);
      if (props.filter == "pending") return props.todos.filter((item) => !item.completed);

      return props.todos;
    });

    return { update, filteredTodos };
  },
};
</script>

<style scoped>
.card {
  padding: 5px;
  border: 1px solid #eee;
  display: flex;
  justify-content: space-between;
}
</style>
