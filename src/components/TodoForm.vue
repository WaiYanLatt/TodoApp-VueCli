<template>
  <form @submit.prevent="addTodo">
    <input
      class="main-input"
      type="text"
      v-model="todoInput"
      placeholder="What needs to be done?"
    />
    <h3 v-show="show === true">No Todos Found</h3>
    <div class="list" v-for="todoItem of filteredTodos" :key="todoItem.id">
      <div>
        <input class="check" type="checkbox" v-model="todoItem.complete" />
        <span class="todoitem" :class="{ line: todoItem.complete === true }">{{
          todoItem.content
        }}</span>
      </div>
      <span class="btn" @click="deleteTodo(todoItem.id)">&times</span>
    </div>
  </form>
  <div class="border">
    <div>
      <h3>({{ getTodo.length }}) items left</h3>
    </div>
    <div>
      <button  @click="setFilterStatus('all')" class="btn2" :class="{ active: filterStatus === 'all' }">
        All
      </button>
      <button  @click="setFilterStatus('active')" class="btn2" :class="{ active: filterStatus === 'active' }">
        Active
      </button>
      <button  @click="setFilterStatus('completed')" class="btn2" :class="{ active: filterStatus === 'completed' }">
        Completed
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todoItems: [{ id: 1, content: "Simple Todo", complete: false }],
      todoInput: "",
      show: false,
      filterStatus: "all",
    };
  },
  watch: {
    todoItems: {
      handler(newValue, oldValue) {
        if (newValue.length === 0) {
          return (this.show = true);
        }
      },
    },
  },
  computed: {
    getTodo() {
      return this.todoItems;
    },
    filteredTodos() {
      if (this.filterStatus === "all") {
        return this.todoItems;
      }
      if (this.filterStatus === "active") {
        return this.todoItems.filter((todoItem) => todoItem.completed === false);
      }
      if (this.filterStatus === "completed") {
        return this.todoItems.filter((todoItem) => todoItem.completed === true);
      }
    },
  },
  methods: {
    addTodo() {
      const newTodo = {
        id: this.todoItems.length + 1,
        content: (this.todoItems.content = this.todoInput),
        complete: false,
      };
      this.todoItems.push(newTodo);
      this.todoInput = "";
      this.show = false;
    },
    deleteTodo(id) {
      this.todoItems = this.todoItems.filter((todoItem) => todoItem.id !== id);
    },
    setFilterStatus(status) {
      this.filterStatus = status;
    },
  },
};
</script>

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

.line {
  text-decoration: line-through;
  text-decoration-color: greenyellow;
  text-decoration-thickness: 0.1rem;
}

.list {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.todoitem {
  color: white;
  font-weight: bold;
  margin-left: 10px;
  font-size: 1.1rem;
}

.btn {
  color: red;
  border-radius: 50%;
  font-size: 2rem;
  cursor: pointer;
  margin-right: 50px;
}

.check {
  width: 50px;
  cursor: pointer;
  accent-color: greenyellow;
}

h3 {
  color: white;
}

.border {
  display: flex;
  align-items: center;
  justify-content: space-between;
  border: 1px solid white;
  padding: 10px;
  border-left: 0px;
  border-right: 0px;
  margin-top: 30px;
}

.btn2 {
  background-color: white;
  border: 0px;
  margin-right: 10px;
  padding: 10px;
  font-weight: bold;
  border-radius: 5px;
  font-size: 1rem;
  cursor: pointer;
}

.active {
  background-color: greenyellow;
  color: white;
}
</style>
