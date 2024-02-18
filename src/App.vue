<template>
  <main class="w-full h-screen bg-gray-200 py-16 px-2">
    <div class="w-full grid grid-cols-3 gap-8">
      <h1 class="font-bold text-2xl col-span-3 text-center">My TODO's App</h1>
      <AddToDoForm @add-todo="handleAddTodo" />

      <div class="col-span-2 flex flex-col gap-8">
        <ToDosList
          v-if="pendingTodos.length"
          title="Pendientes"
          :todos="pendingTodos"
        />
        <ToDosList
          v-if="completedTodos.length"
          title="Completados"
          :todos="completedTodos"
        />

        <button
          class="max-w-min px-8 py-1 border rounded-md bg-slate-600 text-white hover:bg-slate-700 transition-colors duration-300 ease-in-out"
          v-if="todos.length"
          @click="saveToLocalStorage"
        >
          Guardar
        </button>
      </div>
    </div>
  </main>
</template>

<script>
import AddToDoForm from "./components/AddToDoForm.vue";
import ToDosList from "./components/ToDosList.vue";

export default {
  name: "App",
  components: {
    AddToDoForm,
    ToDosList,
  },
  data() {
    return {
      todos: [],
    };
  },
  mounted() {
    const todos = localStorage.getItem("todos");

    if (todos) {
      this.todos = JSON.parse(todos);
    }
  },
  methods: {
    handleAddTodo(newTodo) {
      console.log(newTodo);

      this.todos.push({
        ...newTodo,
        completed: false,
      });
    },
    saveToLocalStorage() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
      this.$toast.success("Tareas guardadas");
    },
  },
  computed: {
    pendingTodos() {
      return this.todos.filter((todo) => !todo.completed);
    },
    completedTodos() {
      return this.todos.filter((todo) => todo.completed);
    },
  },
};
</script>

<style>
@tailwind base;
@tailwind components;
@tailwind utilities;
</style>
