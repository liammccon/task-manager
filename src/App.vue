<template>
  <div id="app">
    <NavBar @addBtnClicked="handleAddClicked" />
    <Tasks :taskList="taskList" @deleteTask="deleteTask" @editTask="editTask"/>
    <!--
      <NewModal ref="newModal" @addTask="addTask"/>
    -->
    <button @click="showNewNewModal">Show new new modal (test)</button>
    <button @click="addTestTask">make a test task (test)</button>
    <div v-if="showNewModal">
      <NewModal2 ref="newModal2" type="NEW" :task="newTask" />
    </div>
    <div v-else>
      <Modal ref="editModal" type="EDIT" :task="taskToEdit"/>
    </div>
  </div>
</template>

<script>
import NavBar from './components/NavBar.vue'
import Tasks from './components/Tasks.vue'
import NewModal from './components/NewModal.vue'
import Modal from './components/Modal.vue'
import NewModal2 from './components/Modal.vue'

export default {
  name: 'App',
  components: {
    NavBar, Tasks, NewModal, Modal, NewModal2
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
    async showNewNewModal(){
      this.showNewModal = true
      this.showEditModal = false
      await new Promise(resolve => setTimeout(resolve, 10)); //Needs to wait a moment or else the modal will be still null
      this.$refs.newModal2.showModal()
    },
     handleAddClicked(){
      this.showNewModal = true
      this.showEditModal = false
      this.$refs.newModal.showModal()
    },
    deleteTask(id){
      this.taskList = this.taskList.filter(t => t.id !== id)
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
          deadline: '2001-02-14',
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
  min-width: 550px;
}
</style>