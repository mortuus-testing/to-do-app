<template>
    <div v-bind:key="task.id" v-for="task in tasks">
        <Task @delete-clicked="$emit('delete-clicked', task.id)" @favorite-clicked="$emit('favorite-clicked', task.id)" @finish-clicked="$emit('finish-clicked', task.id)" :task="task"/>
    </div>
</template>

<script>
import Task from './Task.vue'

export default {
    name: 'Tasks',
    components: {
        Task
    },
    props: {
        tasks: Array
    },
    emits: ['favorite-clicked','delete-clicked','finish-clicked']
}
</script>

<style scoped>
</style>