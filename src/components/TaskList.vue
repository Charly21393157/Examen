<template>
  <div class="task-list">
    <slot name="header"></slot>
    <ul v-if="tasks.length > 0">
      <TaskItem v-for="task in tasks" :key="task.id" :task="task" @complete-task="completeTask" @delete-task="deleteTask" />
    </ul>
    <p v-else>No hay tareas</p>
    <div>
      <input type="text" v-model="newTaskTitle" placeholder="Nombre de la tarea">
      <button @click="addTask">Agregar tarea</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import TaskItem from './TaskItem.vue';
import TasksData from '@/data/TasksData';
import type { ITask } from '@/interfaces/ITask';

const tasks = ref<ITask[]>(TasksData);
const newTaskTitle = ref<string>(''); 

const addTask = () => {
  if (newTaskTitle.value.trim() !== '') {
    const newTask: ITask = {
      id: tasks.value.length + 1,
      title: newTaskTitle.value,
      completed: false,
      description: 'hola Mundo',
      date: new Date()
    };
    tasks.value.push(newTask);
    newTaskTitle.value = '';
  }
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

input[type="text"] {
  margin-right: 10px;
}

button {
  margin-top: 10px;
}
</style>
