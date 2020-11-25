<template>
  <div class="content">
    <div class="heading">
      <h1>Todo List</h1>
    </div>
    <div>
      <md-field>
        <md-input
          v-model="currentTodo"
          @keydown.enter="addTodo()"
          placeholder="Add a todo"
        ></md-input
      ></md-field>
      <ul class="todos" style="list-style:none">
        <li
          v-for="todo in todos"
          :key="todo.id"
          :class="{ isCompleted: todo.completed }"
        >
          <md-card class="md-primary" md-theme="purple-card" md-with-hover>
            <span
              @dblclick="editTodo(todo)"
              class="todo"
              :class="{ isCompleted: todo.completed }"
              :style="{ display: todo.edited }"
              >{{ todo.label }}</span
            >
            <input
              v-model="todo.label"
              @keydown.enter="editTodo(todo)"
              :class="{ isCompleted: todo.completed }"
              :style="{ display: todo.editing }"
              class="editTask"
            />
            <input
              type="checkbox"
              v-model="todo.completed"
              value="completed"
            /><span class="completedlabel">Completed</span>
            <button @click="removeTodo(todo)">Delete</button>
          </md-card>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: "",
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length,
        label: this.currentTodo,
        completed: false,
        edited: "inline-block",
        editing: "none",
      });
      this.currentTodo = "";
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
      todo.edited === "inline-block"
        ? (todo.edited = "none")
        : (todo.edited = "inline-block");
      todo.editing === "inline-block"
        ? (todo.editing = "none")
        : (todo.editing = "inline-block");
    },
  },
};
</script>

<style></style>
