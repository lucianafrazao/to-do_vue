<script setup>
    const props = defineProps(['unfinishedTasks']) 
</script>

<template>
        <header class="p-5 mb-4 bg-light rounded-3">
        <h1>My to do list</h1>
        <p>
            You have {{ props.unfinishedTasks }} unfinished task(s).
        </p>
    </header>
</template>