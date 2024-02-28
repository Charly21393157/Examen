<template>
    <div class="task-list">
      <slot name="header"></slot>
      <ul v-if="tasks.length > 0">
        <TaskItem v-for="task in tasks" :key="task.id" :task="task" @complete-task="completeTask" @delete-task="deleteTask" />
      </ul>
      <p v-else>No hay tareas</p>
      <button @click="addTask">Agregar tarea</button>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref } from 'vue';
  import TaskItem from './TaskItem.vue';
  import TasksData  from '@/data/TasksData';
  import type { ITask } from '@/interfaces/ITask';
  
  const tasks = ref<ITask[]>(TasksData);
  
  const addTask = () => {
    const newTask: ITask = {
      id: tasks.value.length + 1,
      title: 'Nueva tarea',
      completed: false,
      description:'hola Mundo',
      date:new Date()
    };
    tasks.value.push(newTask);
  };
  
  const completeTask = (taskId: number) => {
    const taskIndex = tasks.value.findIndex(task => task.id === taskId);
    if (taskIndex !== -1) {
      tasks.value[taskIndex].completed = true;
    }
  };
  
  const deleteTask = (taskId: number) => {
    const taskIndex = tasks.value.findIndex(task => task.id === taskId);
    if (taskIndex !== -1) {
      tasks.value.splice(taskIndex, 1);
    }
  };
  
  </script>
  
  <style scoped>
  .task-list {
    margin-top: 20px;
  }
  
  ul {
    list-style-type: none;
  }
  
  button {
    margin-top: 10px;
  }
  </style>
  