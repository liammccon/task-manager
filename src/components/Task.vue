<template>
    <div class="container-fluid">
      <div class = "row">
        <div class="col">{{task.title}}</div>
        <div class="col ">{{task.description}}</div>
        <div class="col">{{formattedDate()}}</div>
        <div class="col">{{task.priority}}</div>
        <div class="col">
            <input type="checkbox" class="form-check-input" :id="getCheckboxID()" @click="toggleComplete()">
        </div>
        <div class="col">
          <button v-show="!isComplete" @click="editTask" class="btn btn-primary btn-floating">
            <i class="fa-solid fa-pen-to-square btn-circle"></i>
          </button>
          <button @click="deleteTask" class="btn btn-danger btn-floating">
            <i class="fa-solid fa-trash"></i>
          </button>
        </div>
        <div class="me-2">
          <hr >
        </div>
        
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Task',
    data () {
      return {
        isComplete: false,
      }
    }, 
    props: {
      task: Object
    },
    emits: ["deleteTask", "editTask"],
    methods: {
      deleteTask(){
        this.$emit('deleteTask', this.task.id)
      },
      editTask(){
        this.$emit('editTask', this.task.id)
      },
      toggleComplete(){
        console.log(this.task.complete)
        this.isComplete = $("#" + this.getCheckboxID()).prop("checked")
      },
      getCheckboxID(){
        return  "checkbox" + this.task.id
      },
      formattedDate(){
        return new Date(this.task.deadline).toLocaleDateString('en-us', { year:"numeric", month:"numeric", day:"numeric"}) 
      }
    }
  
  };
  
  </script>
  
  <style scoped>
  
  </style>