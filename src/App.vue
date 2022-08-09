<template>
  <AddTask @submit-clicked="onSubmit"/>
  <Tasks @delete-clicked="onDelete" @finish-clicked="onFinish" @favorite-clicked="onFavorite" :tasks="tasks"/>
</template>

<script>
  import AddTask from './components/AddTask.vue'
  import Tasks from './components/Tasks.vue'

  export default {
    name: 'App',
    components: {
      AddTask,
      Tasks
    },
    data() {
      return {
        tasks: []
      }
    },
    methods: {
      async getSpecificData(id) {
        const res = await fetch(`https://mortuus-json-fake-server.herokuapp.com/tasks/${id}`)
        const data = await res.json()
        return data
      },
      async onFavorite(id) {
        const data = await this.getSpecificData(id)
        const updated_data = await {...data, favorite : !data.favorite}
        const res = await fetch(`https://mortuus-json-fake-server.herokuapp.com/tasks/${id}`, {
          method: 'PUT',
          headers: {
            'Content-Type' : 'application/json'
          },
          body: JSON.stringify(updated_data)
        })
        this.tasks = this.tasks.map((task) => task.id === id ? {...task, favorite: !task.favorite} : task)
      },
      async onFinish(id) {
        const data = await this.getSpecificData(id)
        const updated_data = await {...data, finish : !data.finish}
        const res = await fetch(`https://mortuus-json-fake-server.herokuapp.com/tasks/${id}`, {
          method: 'PUT',
          headers: {
            'Content-Type' : 'application/json'
          },
          body: JSON.stringify(updated_data)
        })
      },
      async onDelete(id) {
        if (confirm("Are you sure?")) {
          const res = await fetch(`https://mortuus-json-fake-server.herokuapp.com/tasks/${id}`, {
            method: 'DELETE'
          })
          this.tasks = this.tasks.filter((task) => task.id !== id)   
        }
      },
      async onSubmit(task) {
        const res = await fetch("https://mortuus-json-fake-server.herokuapp.com/tasks", {
          method: 'POST',
          headers: {'Content-Type' : 'application/json'},
          body: JSON.stringify(task)
        })
        const data = await res.json()
        this.tasks = [...this.tasks, data]
      }
    },
    async created() {
      const res = await fetch("https://mortuus-json-fake-server.herokuapp.com/tasks")
      const data = await res.json()
      this.tasks = await data
    }
  }
</script>

<style>
  body {
    background-color: #666666;
  }
</style>