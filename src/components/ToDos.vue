<template>
  <SingleTodo @updateLS="update" :todo="todo" v-for="todo in filteredTodos" :key="todo.id" />
  <AddTodo @updateLS="update" />
</template>

<script>
import SingleTodo from "@/components/SingleTodo.vue";
import AddTodo from "@/components/AddTodo.vue";

import { computed, ref } from "@vue/runtime-core";
export default {
  props: ["filter"],
  components: { SingleTodo, AddTodo },
  setup(props) {
    const toDos = ref(JSON.parse(localStorage.toDos));
    const update = () => {
      toDos.value = JSON.parse(localStorage.toDos);
    };

    const filteredTodos = computed(() => {
      if (props.filter == "completed") return toDos.value.filter((item) => item.completed);
      if (props.filter == "pending") return toDos.value.filter((item) => !item.completed);

      return toDos.value;
    });

    return { update, filteredTodos };
  },
};
</script>
