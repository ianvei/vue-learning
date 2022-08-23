<script>
  import HeaderVue from './components/Header.vue';
  import Tasks from './components/Tasks.vue'


  export default {
    name: 'App',
    components: {
    HeaderVue,
    Tasks
},
    data() {
      return {
        tasks: []
      }
    },
    methods:{
      deleteTask(id){
        console.log('task', id);
        this.tasks = this.tasks.filter((task) => task.id !== id)
      }
    },
    created(){
      this.tasks = [
        {
          id: 1,
          text: 'doctors appointment',
          day: 'march 1st 2:30pm',
          reminder: true,
        },
        {
          id: 2,
          text: 'doctors appointment2',
          day: 'march 2st 2:30pm',
          reminder: true,
        },
        {
          id: 3,
          text: 'doctors appointment3',
          day: 'march 3st 2:30pm',
          reminder: false,
        },
      ]
    },
    

  }
</script>

<template>
  <div class="container">
    <HeaderVue title="Task Tracker"/>
    <Tasks @delete-task="deleteTask" :tasks="tasks"/>
  </div>
  
</template>

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
