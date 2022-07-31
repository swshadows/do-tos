<template>
  <div class="notfound">
    <h1>ERROR</h1>
    <h4>Page not found 💀</h4>
    <router-link to="/">Go back to homepage</router-link>
  </div>
</template>

<style scoped>
.notfound {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 100px;
}
.notfound h1 {
  color: #ff0000;
}
a {
  color: #9c6ebb;
}
</style>
