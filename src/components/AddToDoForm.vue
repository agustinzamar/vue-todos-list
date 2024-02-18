<template>
  <div class="bg-white rounded-md p-4 flex flex-col gap-4 min-w-[300px]">
    <h2 class="font-bold text-sm">Nuevo TODO</h2>
    <input
      type="text"
      v-model="newTodo.title"
      class="border rounded-md p-2 mt-2"
      placeholder="Título de la tarea"
    />
    <textarea
      v-model="newTodo.body"
      name="body"
      id="body"
      cols="30"
      rows="10"
      placeholder="Descripción de la tarea"
      class="resize-none border rounded-md p-2 mt-2"
    ></textarea>
    <button
      @click="addTodo"
      class="px-2 py-1 border rounded-md bg-slate-600 text-white hover:bg-slate-700 transition-colors duration-300 ease-in-out"
    >
      Agregar
    </button>
  </div>
</template>

<script>
export default {
  name: "AddToDoForm",
  data() {
    return {
      newTodo: {
        title: "",
        body: "",
      },
    };
  },
  methods: {
    addTodo() {
      this.$emit("add-todo", this.newTodo);
      this.newTodo = {
        title: "",
        body: "",
      };
    },
  },
};
</script>
