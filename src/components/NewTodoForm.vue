<script>
export default {
  emits: ["submitTodo"],
  data() {
    return {
      todoTitle: "",
    };
  },
};
</script>
<template>
  <form action="#" @submit.prevent="$emit('submitTodo', todoTitle)">
    <input
      class="main-input"
      type="text"
      v-model="todoTitle"
      placeholder="What needs to be done?"
    />
  </form>
</template>
<style scoped>
.main-input {
  width: 500px;
  border-radius: 5px;
  outline: 0;
  border: 1px solid white;
  padding: 10px;
  height: 25px;
  font-size: 1.2rem;
  font-weight: 500;
}
</style>
