<template>
  <div class="container">
    <HeaderVue @toggle-add-task="toggleAddTask" :showAddTask="showAddTask" title="Task Tracker"/>
    <AddTask v-if="showAddTask" @add-task="addTask" />
    <Tasks  @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks"/>
  </div>
</template>

<script>
  import HeaderVue from './components/Header.vue';
  import Tasks from './components/Tasks.vue'
  import AddTask from './components/AddTask.vue';
  import TaskVue from './components/Task.vue';


  export default {
    name: 'App',
    components: {
    HeaderVue,
    Tasks,
    AddTask
},
    data() {
      return {
        tasks: [],
        showAddTask: false,
      }
    },
    methods:{
      async deleteTask(id){
        console.log('task', id);

        const res = await fetch(`http://localhost:5000/tasks/${id}`, {
          method: 'DELETE',
        })
        
        res.status === 200 ? this.tasks = this.tasks.filter((task) => task.id !== id) : alert('Error deleting task')
      },
      async toggleReminder(id){
        const taskToToggle = await this.fetchTask(id);
        const updTask = {...taskToToggle, reminder: !taskToToggle.reminder};

        const res = await fetch(`http://localhost:5000/tasks/${id}`, {
          method: 'PUT',
          headers: {
            'Content-type': 'application/json',
          },
          body: JSON.stringify(updTask),
        }) 

        const data = await res.json() 
        console.log('reminder',id)
        this.tasks = this.tasks.map((task) => task.id === id? {...task, reminder: data.reminder} : task)
      },
      async addTask(task){
        console.log(task)
        const res = await fetch('http://localhost:5000/tasks', {
          method: 'POST',
          headers: {
            'Content-type': 'application/json',
          },
          body: JSON.stringify(task),
        })
        
        const data = await res.json()
        console.log('hi')
        this.tasks = [...this.tasks, data]
      },
      toggleAddTask() {
        this.showAddTask = !this.showAddTask;
      },
      async fetchTasks(){
        const response = await fetch('http://localhost:5000/tasks');
        const data = await response.json()
        return data
      },
      async fetchTask(id){
        const response = await fetch(`http://localhost:5000/tasks/${id}`);
        const data = await response.json()
        return data
      },
    },
    async created(){
      this.tasks = await this.fetchTasks();
    },
    emits: ['add-task']

  }
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.container > header > button {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
button {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
