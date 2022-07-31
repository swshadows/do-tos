<template>
  <div v-if="add">
    <form @submit.prevent="handleSubmit">
      <input type="text" placeholder="Titulo" v-model="title" />
      <textarea v-model="body" placeholder="Corpo"> </textarea>
      <button>Adicionar novo to-do</button>
      <button class="minus" @click="add = !add">Fechar</button>
    </form>
  </div>
  <div class="addNew" v-else>
    <button @click="add = !add">Adicionar novo to-do</button>
  </div>
</template>

<script>
import { ref } from "@vue/reactivity";

export default {
  setup(props, { emit }) {
    const add = ref(false);
    const title = ref("");
    const body = ref("");

    const handleSubmit = () => {
      if (title.value && body.value) {
        const toDos = JSON.parse(localStorage.toDos);
        const todo = {
          id: toDos.length,
          title: title.value,
          body: body.value,
          completed: false,
        };
        toDos.push(todo);
        localStorage.toDos = JSON.stringify(toDos);
        emit("updateLS");
      }
      title.value = "";
      body.value = "";
    };

    return { title, body, handleSubmit, add };
  },
};
</script>

<style scoped>
form {
  display: flex;
  padding: 10px;
  margin: 0 auto;
  flex-direction: column;
  gap: 10px;
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
  background: #52ffd9;
  border: 1px solid #fff;
  cursor: pointer;
  padding: 0.4rem;
  transition: 0.2s all;
}
button:hover {
  color: #fff;
  background: #258570;
}
button.minus {
  background: #ff4646;
}
button.minus:hover {
  background: #8d2b2b;
}
.addNew {
  display: flex;
  padding: 10px;
  flex-direction: column;
}
</style>
