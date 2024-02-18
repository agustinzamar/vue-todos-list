<template>
  <div class="flex flex-col gap-2">
    <h3 class="text-lg font-semibold">{{ title }}</h3>
    <ul class="flex flex-col gap-2">
      <li v-for="todo in todos" :key="todo.title">
        <label class="font-semibold flex flex-row items-center gap-4">
          <input type="checkbox" class="w-6 h-6" v-model="todo.completed" />

          <p class="flex flex-col">
            <strong> {{ todo.title }} </strong>

            {{ todo.body }}
          </p>
        </label>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "ToDosList",
  props: {
    title: {
      type: String,
      required: true,
    },
    todos: {
      type: Array,
      required: true,
    },
  },
};
</script>
