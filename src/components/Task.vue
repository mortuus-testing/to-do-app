<template>
    <div :class="[task.finish ? 'finished' : '', 'main-container']">
        <div>
            <input v-model="task.finish" type="checkbox" @click="$emit('finish-clicked', task.id)">
            <p class="msg">{{task.msg}}</p>
        </div>
        <div>
            <div @click="$emit('delete-clicked', task.id)" class="fa fa-trash-o"></div>
            <div v-on:click="$emit('favorite-clicked', task.id)" :class="[task.favorite ? 'fa fa-star favorited' : 'fa fa-star-o']"></div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Task',
    props: {
        task: Object
    }
}
</script>

<style scoped>
    .main-container {
        display: flex;
        justify-content: space-between;
        align-items: center;
        border: 1px solid white;
        padding: 0 10px;
        margin: 0 10px;
    }
    .main-container div {
        display: flex;
        align-items: center;
    }
    input {
        min-width: 20px;
        min-height: 20px;
        margin: 10px 10px;
    }
    .fa {
        color: #dddddd;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 22px;
        margin: 5px 13px;
    }
    .finished {
        opacity: 0.4;
    }
    .favorited {
        color: orange;
    }
    .fa-star-o:hover {
        color: orange;
    }
    .fa-trash-o:hover {
        color: #ff8888;
    }
    .fa-edit:hover {
        color: #88ff88;
    }
    p {
        color: white;
    }
</style>