<template>
    <form @submit="onSubmit">
        <input type="text" v-model="msg">
        <input class="submit" type="submit" value="Add Task">
    </form>
</template>

<script>
    export default {
        name: 'AddTask',
        data() {
            return {
                msg: ""
            }
        },
        methods: {
            onSubmit(e) {
                e.preventDefault()
                if (!this.msg) {
                    alert("Please add a task!")
                    return
                }

                const newTask = {
                    msg: this.msg,
                    finish: false,
                    favorite: false
                }
                this.$emit('submit-clicked', newTask)
                this.msg = ""
            }
        }
    }
</script>

<style scoped>
    form {
        width: 100vw;
        height: 30vh;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    input {
        height: 30px;
        width: 400px;
        padding-left: 20px;
    }
    .submit {
        height: 30px;
        width: 100px;
        padding: 5px;
        font-size: 15px;
        font-weight: bold;
        color: white;
        background-color: #0EAD69;
        border: none;
    }
    .submit:hover {
        opacity: 0.8;
    }
</style>