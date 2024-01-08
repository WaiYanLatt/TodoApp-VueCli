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
      // Making sure that the todoTitle is not empty
      if (todoTitle.trim() === "") {
        alert("Please enter a todo title");
        return; // This will exit the function and prevent the code below from running
      }
      // Create a new todo object
      const newTodo = {
        id: this.todos.length + 1, // Generate a unique id
        title: todoTitle,
        completed: false,
      };
      // Add the new todo to the todos array
      this.todos.push(newTodo);
      // Reset the todoTitle property to an empty string using the $refs property
      this.$refs.todoInput.todoTitle = "";
    },
    deleteTodo(id) {
      // Find the index of the todo with the given id
      const index = this.todos.findIndex((todo) => todo.id === id);
      // Remove the todo from the todos array
      this.todos.splice(index, 1);
    },
    toggleTodo(id) {
      // Find the index of the todo with the given id
      const index = this.todos.findIndex((todo) => todo.id === id);
      // Toggle the completed property of the todo
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
  <TodoFilters :filterStatus="filterStatus" :totalTodos="totalTodos" @setFilter="setFilterStatus" />
</template>



<style scoped>
.todo-list {
  list-style: none;
  padding: 0;
}
</style>
