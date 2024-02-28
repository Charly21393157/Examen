<template>
    <li :class="{ 'completed': task.completed }">
      <input type="checkbox" v-model="task.completed" @change="completeTask" />
      <span>{{ task.title }}</span>
      <button @click="deleteTask">Eliminar</button>
    </li>
  </template>
  
  <script setup lang="ts">
  // import { defineProps, defineEmits } from 'vue';
  import type { ITask } from '@/interfaces/ITask';
  
  const props = defineProps<{ task: ITask }>();
  const emits = defineEmits(['complete-task', 'delete-task']);
  
  const completeTask = () => {
    emits('complete-task', props.task.id);
  };
  
  const deleteTask = () => {
    emits('delete-task', props.task.id);
  };
  
  </script>
  
  <style scoped>
  .completed {
    text-decoration: line-through;
  }
  </style>
  