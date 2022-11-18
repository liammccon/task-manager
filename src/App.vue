<template>
  <div id="app">
    <NavBar @addBtnClicked="handleAddClicked" />
    <Tasks :taskList="taskList" @deleteTask="deleteTask" @editTask="editTask"/>
    <NewModal ref="newModal" @addTask="addTask"/>
    <Modal ref="editModal" type="EDIT" :task="taskToEdit"/>
    <Modal ref="newModal2" type="NEW" :task="createEmptyTask()"/>
  </div>
</template>

<script>
import NavBar from './components/NavBar.vue'
import Tasks from './components/Tasks.vue'
import NewModal from './components/NewModal.vue'
import Modal from './components/Modal.vue'

export default {
  name: 'App',
  components: {
    NavBar, Tasks, NewModal, Modal
  },
  methods: {
    handleAddClicked(){
      this.$refs.newModal.showModal()
    },
    deleteTask(id){
      this.taskList = this.taskList.filter(t => t.id !== id)
    },
    editTask(id){
      this.taskToEdit = this.taskList.find(task => task.id=id)
      this.$refs.editModal.showModal()
    },
    addTask(task){
      task.id=this.nextID++
      this.taskList.push(task)
    },
    createEmptyTask(){
      return {
          id: this.nextID++, //Increment ID for each task
          title: '',
          description: '',
          deadline: '',
          priority: '',
          complete: false,
      }
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
      taskToEdit: Object,
      editOrNew: String
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