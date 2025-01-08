<script setup>
  import { reactive } from 'vue';
  import Header from './components/Header.vue';
  import Forms from './components/Forms.vue';
  import ToDoList from './components/ToDoList.vue';

  const state = reactive({
    filtering: 'all',
    tempTask: '',
    tasks: [
      {
        title: 'Study EBAC',
        done: false,
      },
      {
        title: 'Go to the gym',
        done: true,
      },
      {
        title: 'Take car to the shop',
        done: true,
      }
    ]
  })

  const getUnfinishedTasks = () => {
    return state.tasks.filter(task => !task.done)
  }

  const getFinishedTasks = () => {
    return state.tasks.filter(task => task.done)
  }

  const getFilteredTasks = () => {
    const { filtering } = state;

    switch (filtering) {
      case 'unfinished':
        return getUnfinishedTasks();
      case 'finished':
        return getFinishedTasks();
      default:
        return state.tasks;
    }
  }

  const addTask = () => {
    const newTask = {
      title: state.tempTask,
      done: false,
    }
    state.tasks.push(newTask);
    state.tempTask = '';
  }
</script>

<template>
  <div class="container">
    <Header :unfinished-tasks="getUnfinishedTasks().length" />
    <Forms :change-filter="event => state.filtering = event.target.value" :temp-task="state.tempTask" :edit-temp-task="event => state.tempTask = event.target.value" :add-task="addTask"/>
    <ToDoList :tasks="getFilteredTasks()" />
  </div>
</template>

<style scoped>
  .taskDone {
    text-decoration: line-through;
  }
</style>
