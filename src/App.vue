<script setup>
import { reactive } from 'vue';

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
    <header class="p-5 mb-4 bg-light rounded-3">
      <h1>My to do list</h1>
      <p>
        You have {{ getUnfinishedTasks().length }} unfinished task(s).
      </p>
    </header>
    <form @submit.prevent="addTask">
      <div class="row">
        <div class="col">
          <input :value="state.tempTask" @change="event => state.tempTask = event.target.value" required type="text" placeholder="Task description" class="form-control"></div>
          <div class="col-md-1">
            <button type="submit" class="btn btn-primary">Add</button>
          </div>
          <div class="col-md-2">
            <select @change="event => state.filtering = event.target.value" class="form-control">
              <option value="all">All tasks</option>
              <option value="unfinished">Unfinished tasks</option>
              <option value="finished">Finished tasks</option>
              <p></p>
            </select>
          </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="task in getFilteredTasks()">
        <input @change="event => task.done = event.target.checked" :checked="task.done" :id="task.title" type="checkbox">
        <label :class="{ taskDone: task.done}" class="ms-3">
          {{ task.title }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .taskDone {
    text-decoration: line-through;
  }
</style>
