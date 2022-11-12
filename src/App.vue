<template>
  <div class="hello">
    <h2>Todo app</h2>
    <button style="submit" @click="deleteAll()">DeleteAll</button>

    <h3>Enter todo</h3>
    <p>Name:</p>
    <input v-model="todo.name" />
    <p>Description:</p>
    <input v-model="todo.description" />
    <p>Deadline:</p>
    <input v-model="todo.deadline" />
    <br /><br />
    <button style="submit" @click="create">Create</button>
    <hr />
    <button style="submit" @click="read">Read</button>
    <hr />
    <div v-for="todo in todos" :key="todo.name">
      <li>Name: {{ todo.name }}</li>
      <li>Description: {{ todo.description }}</li>
      <li>Deadline: {{ todo.deadline }}</li>
      <button style="submit" @click="deleteTodo(todo)">Delete</button>
      <hr />
    </div>
  </div>
</template>

<script>
// import HelloWorldVue from "./components/HelloWorld.vue";
export default {
  name: "App",
  data: () => ({
    todos: [],
    todo: {
      name: "",
      description: "",
      deadline: "",
    },
    name: "todos",
  }),
  methods: {
    read() {
      const data = (this.todos = sessionStorage.getItem(this.name));
      if (data) {
        this.todos = JSON.parse(data);
      }
    },
    create() {
      this.todos.push(this.todo);
      sessionStorage.setItem(this.name, JSON.stringify(this.todos));
      this.todo = {
        name: "",
        description: "",
        deadline: "",
      };
    },
    deleteTodo(todo) {
      // trueのアイテムだけtodos に戻す
      this.todos = this.todos.filter((item) => item.name !== todo.name);
      sessionStorage.setItem(this.name, JSON.stringify(this.todos));
    },
    deleteAll() {
      sessionStorage.clear();
      this.todos = [];
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
