<template>
  <div id="app">
    <NavBar @addBtnClicked="handleAddClicked" />
    <div class="ltm-content">
      <Tasks :taskList="taskList" @deleteTask="deleteTask" @editTask="editTask"/>
      <div v-if="showNewModal">
        <NewModal ref="newModal" type="NEW" :task="newTask" 
        :currentTitles="this.taskList.map(task  => task.title)" 
        @addTask="addTask"/>
      </div>
      <div v-else>
        <EditModal ref="editModal" type="EDIT" :task="taskToEdit" @updateTask="updateTask"/>
      </div>
    </div>
    
  </div>
</template>

<script>
import NavBar from './components/NavBar.vue'
import Tasks from './components/Tasks.vue'
import EditModal from './components/Modal.vue'
import NewModal from './components/Modal.vue'

export default {
  name: 'App',
  components: {
    NavBar, Tasks, EditModal, NewModal
  },
  computed: {
    makeNewTask() {
        return {
              id: this.nextID++, //Increment ID for each task
              title: '',
              description: '',
              deadline: '',
              priority: '',
              complete: false,
          }
    },
  } ,
  methods: {
    async openNewModal(){
      this.showNewModal = true
      this.showEditModal = false
      await new Promise(resolve => setTimeout(resolve, 10)); //Needs to wait a moment or else the modal will be still null
      this.$refs.newModal.showModal()
    },
     handleAddClicked(){
      this.openNewModal()
    },
    deleteTask(id){
      let taskToDelete = this.taskList.filter(t => t.id === id)[0]
      this.taskList = this.taskList.filter(t => t.id !== id)
      toastr.success('Deleted task: ' + taskToDelete.title)
    },
    async editTask(id){
      this.taskToEdit = this.taskList.find(task => task.id == id)
      this.showNewModal = false
      this.showEditModal = true
      await new Promise(resolve => setTimeout(resolve, 10)); //Needs to wait a moment or else the modal will be still null
      this.$refs.editModal.showModal()
    },
    addTask(task){
      task.id=this.nextID++
      this.taskList.push(task)
      toastr.success("Added new task: " + task.title)
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
    updateTask(editedTask){
      let taskToUpdate = this.taskList.find(task => task.id == editedTask.id)
      taskToUpdate.description = editedTask.description
      taskToUpdate.deadline = editedTask.deadline
      taskToUpdate.priority = editedTask.priority
      toastr.success("Edited task: " + taskToUpdate.title)
    },
    listOfCurrentTitles(){
      return this.taskList.map(task  => task.title)
    },
    addTestTask(){

      this.taskList.push(
        {
          id: this.nextID++, //Increment ID for each task
          title: 'MyTitle',
          description: 'MyDescription',
          deadline: '2001-02-14',
          priority: 'med',
          complete: true,
        }
      )
    },
  },
  data (){
    return {
      taskList: [],
      nextID: 1,
      newTask: Object,
      taskToEdit: Object, //Invalid by default, must change to use
      editOrNew: String,
      newTask:
          {
              id: this.nextID++, //Increment ID for each task
              title: '',
              description: '',
              deadline: '',
              priority: '',
              complete: false,
          },
      showNewModal: false,
      showEditModal: false,
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
  min-width: 500px;
}
</style>