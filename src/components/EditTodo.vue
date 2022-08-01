<template>
  <form @submit.prevent="handleSubmit">
    <input type="text" placeholder="Titulo da tarefa" v-model="title" />
    <textarea placeholder="Descrição da tarefa" v-model="body"> </textarea>
    <button>Editar tarefa # {{ todo.id }}</button>
    <button class="cancel" @click="handleEditMode">Cancelar</button>
  </form>
</template>

<script>
import { ref } from "@vue/reactivity";
export default {
  props: ["todo"],
  emits: ["changeEdit", "updateLS"],
  setup(props, { emit }) {
    const title = ref(props.todo.title);
    const body = ref(props.todo.body);

    const handleEditMode = () => {
      emit("changeEdit");
    };

    const handleSubmit = () => {
      if (title.value && body.value) {
        const toDos = JSON.parse(localStorage.toDos);

        toDos.map((item) => {
          if (item.id == props.todo.id) {
            item.title = title.value;
            item.body = body.value;
          }
        });

        localStorage.toDos = JSON.stringify(toDos);
        emit("updateLS");
        emit("changeEdit");
      }
    };

    return { title, body, handleEditMode, handleSubmit };
  },
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  width: 100%;
}
input,
textarea {
  border: 1px solid #eee;
  outline: 0;
  padding: 0.3rem;
}
input:focus,
textarea:focus {
  border-color: #aaa;
}
textarea {
  resize: vertical;
}
button {
  background: #d882d8;
  border: 1px solid #fff;
  cursor: pointer;
  padding: 0.4rem;
  transition: 0.2s all;
}
button:hover {
  color: #fff;
  background: #7c2d7c;
}
button.cancel {
  background: #ff4646;
}
button.cancel:hover {
  background: #8d2b2b;
}
</style>
