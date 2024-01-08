<script>
import NewTodoForm from "@/components/NewTodoForm.vue";
import TodoItem from "@/components/TodoItem.vue";
import TodoFilters from "@/components/TodoFilter.vue";
export default {
  components: {
    NewTodoForm,
    TodoItem,
    TodoFilters,
  },
  data() {
    return {
      todos: [],
      filterStatus: "all",
    };
  },
  computed: {
    filteredTodos() {
      if (this.filterStatus === "all") {
        return this.todos;
      } else if (this.filterStatus === "active") {
        return this.todos.filter((todo) => todo.completed === false);
      } else if (this.filterStatus === "completed") {
        return this.todos.filter((todo) => todo.completed === true);
      }
    },
    totalTodos() {
      return this.filteredTodos.length;
    },
  },
  methods: {
    addTodo(todoTitle) {
      if (todoTitle.trim() === "") {
        alert("Please enter a todo title");
        return;
      }
      // Create a new todo object
      const newTodo = {
        id: this.todos.length + 1,
        title: todoTitle,
        completed: false,
      };
      this.todos.push(newTodo);
      this.$refs.todoInput.todoTitle = "";
    },
    deleteTodo(id) {
      const index = this.todos.findIndex((todo) => todo.id === id);
      this.todos.splice(index, 1);
    },
    toggleTodo(id) {
      const index = this.todos.findIndex((todo) => todo.id === id);
      this.todos[index].completed = !this.todos[index].completed; // This will set it to the opposite of what it currently is (true to false and false to true)
    },
    setFilterStatus(status) {
      this.filterStatus = status;
    },
  },
};
</script>

<template>
  <NewTodoForm ref="todoInput" @submitTodo="addTodo" />
  <ul class="todo-list">
    <TodoItem
      v-for="todo in filteredTodos"
      :key="todo.id"
      :title="todo.title"
      :completed="todo.completed"
      @removeTodo="deleteTodo(todo.id)"
      @toggleTodo="toggleTodo(todo.id)"
    />
  </ul>
  <TodoFilters
    :filterStatus="filterStatus"
    :totalTodos="totalTodos"
    @setFilter="setFilterStatus"
  />
</template>

<style scoped>
.todo-list {
  list-style: none;
  padding: 0;
}
</style>
