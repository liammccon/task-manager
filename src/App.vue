<template>
  <div id="app">
    <NavBar @addBtnClicked="handleAddClicked" />
    <Tasks :taskList="taskList" @deleteTask="deleteTask" />
    <NewModal/>
  </div>
</template>

<script>
import NavBar from './components/NavBar.vue'
import Tasks from './components/Tasks.vue'
import NewModal from './components/NewModal.vue'

export default {
  name: 'App',
  components: {
    NavBar, Tasks, NewModal,
  },
  methods: {
    handleAddClicked(){
      this.addTestTask()
    },
    deleteTask(id){
      this.taskList = this.taskList.filter(t => t.id !== id)
    },
    
    addTestTask(){

      this.taskList.push(
        {
          id: this.nextID++, //Increment ID for each task
          title: 'MyTitle',
          description: 'MyDescription',
          deadline: '02-14-2001',
          priority: 'med',
          complete: true,
        }
      )
    }
  },
  data (){
    return {
      taskList: [],
      nextID: 1,
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  min-width: 550px;
}
</style>