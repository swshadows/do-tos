<template>
  <div class="card" v-if="!editMode">
    <router-link :to="{ name: 'todo', params: { id: todo.id } }">
      <h1>
        <span v-if="todo.completed">✅</span>
        <span v-else>❌</span>
        {{ reducedTitle }}
      </h1>
    </router-link>
    <div class="options">
      <button v-if="!todo.completed" @click="handleDone(todo.id)" class="done">✔ <span>Concluido?</span></button>
      <button v-else @click="handleDone(todo.id)" class="pending">✖ <span>Pendente?</span></button>
      <button @click="editMode = !editMode" class="edit">✏ <span>Editar?</span></button>
      <button @click="handleDelete(todo.id)" class="delete">🗑 <span>Deletar?</span></button>
    </div>
  </div>
  <div class="card" v-else>
    <EditTodo @updateLS="handleEdit" @changeEdit="editMode = !editMode" :todo="todo" />
  </div>
</template>

<script>
import EditTodo from "@/components/EditTodo.vue";
import { computed, ref } from "@vue/runtime-core";
export default {
  props: ["todo"],
  emits: ["updateLS"],
  components: { EditTodo },
  setup(props, { emit }) {
    const editMode = ref(false);

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

    const handleEdit = () => {
      emit("updateLS");
    };

    const reducedTitle = computed(() => {
      if (props.todo.title.length > 20) return props.todo.title.slice(0, 20) + "...";
      return props.todo.title;
    });
    return { editMode, reducedTitle, handleDone, handleDelete, handleEdit };
  },
};
</script>

<style scoped>
.card {
  display: flex;
  justify-content: space-between;
  padding: 5px;
  border: 1px solid #eee;
}
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
  display: flex;
  justify-content: center;
  gap: 5px;
  padding: 5px;
  cursor: pointer;
  color: #fff;
  width: 40px;
  transition: 0.1s all;
}
button:hover {
  width: 100px;
}
button span {
  display: none;
}
button:hover span {
  display: inline;
}
button.done {
  background: #258570;
}
button.pending {
  background: #b6921c;
}
button.edit {
  background: #1cacb6;
}
button.delete {
  background: #ff4646;
}
</style>
