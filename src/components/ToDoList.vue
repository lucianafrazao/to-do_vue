<script setup>
const props = defineProps(['tasks'])
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="task in props.tasks">
            <input @change="event => task.done = event.target.checked" :checked="task.done" :id="task.title"
                type="checkbox">
            <label :class="{ taskDone: task.done }" class="ms-3">
                {{ task.title }}
            </label>
        </li>
    </ul>
</template>

<style scoped>
    .taskDone {
        text-decoration: line-through;
    }
</style>