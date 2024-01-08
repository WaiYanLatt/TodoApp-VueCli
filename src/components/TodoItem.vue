<script>
export default {
  emits: ["removeTodo", "toggleTodo"],
  props: {
    title: {
      type: String,
      required: true,
    },
    completed: Boolean,
  },
};
</script>
<template>
  <li class="list">
    <div>
      <input
        type="checkbox"
        @change="$emit('toggleTodo')"
        :checked="completed"
      />
      <span class="todo-title todoitem" :class="{ completed: completed }">{{
        title
      }}</span>
    </div>
    <div class="btn" @click="$emit('removeTodo')">x</div>
  </li>
</template>
<style scoped>
.todoitem {
  color: white;
  font-weight: bold;
  margin-left: 20px;
  font-size: 1.2rem;
}

.list {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-left: 20px;
}

input:checked {
  accent-color: greenyellow;
}

.todo-title.completed {
  text-decoration: line-through;
  text-decoration-color: greenyellow;
  text-decoration-thickness: 0.1rem;
}

.btn {
  color: red;
  border-radius: 50%;
  font-size: 1.5rem;
  cursor: pointer;
  margin-right: 50px;
  font-weight: 600;
}
</style>
