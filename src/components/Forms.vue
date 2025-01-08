<script setup>
    const props = defineProps(['addTask', 'tempTask', 'changeFilter', 'editTempTask'])
</script>

<template>
    <form @submit.prevent="props.addTask">
        <div class="row">
            <div class="col">
                <input :value="props.tempTask" @change="props.editTempTask" required
                    type="text" placeholder="Task description" class="form-control">
            </div>
            <div class="col-md-1">
                <button type="submit" class="btn btn-primary">Add</button>
            </div>
            <div class="col-md-2">
                <select @change="props.changeFilter" class="form-control">
                    <option value="all">All tasks</option>
                    <option value="unfinished">Unfinished tasks</option>
                    <option value="finished">Finished tasks</option>
                    <p></p>
                </select>
            </div>
        </div>
    </form>

</template>