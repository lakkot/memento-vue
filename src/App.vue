<template>

  <div class="content">
    <input class ="todo-input" v-model="currentTodo" @keydown.enter="addTodo()" placeholder="add a todo">
      <ul class="todos">
        <li v-for="todo in todos" :key="todo.id">
          <div v-if="todo.edit === false" :class="{completed : todo.completed === 'completed'}">
            <div  @dblclick="editTodo(todo)">
              {{ todo.label }}
            </div>
            <input type="checkbox" @click="completeTodo(todo)" >
            {{todo.completed}}
            <button @click="removeTodo(todo)">Delete</button>
          </div>
          <div v-if="todo.edit">
              <input v-model="todo.label" @keydown.enter="stopEditTodo(todo)" placeholder="enter new todo name">
          </div>
        </li>
      </ul>
  </div>

</template>

<script>

export default {
  data() {
    return {
      todos: [],
      currentTodo: '',
    };
  },
  methods: {
    addTodo() {
      this.todos.push({id: this.todos.length, label: this.currentTodo, completed: "pending", edit: false});
      this.currentTodo = '';
      console.log(this.todos)
    },
    completeTodo(todo) {
      const index = this.todos.indexOf(todo);
      if (this.todos[index].completed === "pending") {
      this.todos[index].completed = "completed";
      } else {
      this.todos[index].completed = "pending";

      }
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.editedTodo = index;
      this.todos[index].edit = true;
      console.log(this.todos[index])
      console.log(this.editedTodo);
    },
    stopEditTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos[index].edit = false;
    },
  }
};

</script>

<style>

.content {
  border: 1px solid black;
}

.completed {
  color: darkgreen;
}

</style>
