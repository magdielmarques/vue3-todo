<script lang="ts">
import { ref } from "vue";

export default {
  setup() {
    const tasks = ref([]);
    const newTask = ref({
      name: "",
      isCompleted: false,
    });
    function addTask() {
      tasks.value.push({ ...newTask.value });
      newTask.value.name = "";
    }
    function markTaskCompleted(position: number) {
      tasks.value[position].isCompleted = !tasks.value[position].isCompleted;
    }
    return {
      tasks,
      addTask,
      markTaskCompleted,
      newTask,
    };
  },
};
</script>

<template>
  <h1>Todo List</h1>
  <input v-model="newTask.name" type="text" placeholder="Task Name" />
  <button @click="addTask()" type="submit">Add</button>
  <ul>
    <li v-for="(task, index) in tasks" :key="index">
      <input
        @click="markTaskCompleted(index)"
        type="checkbox"
        :checked="task.isCompleted"
      />
      {{ task.name }}
    </li>
  </ul>
</template>
