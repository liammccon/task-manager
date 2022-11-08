<template>
    <div class="container-fluid">
      <div class = "row">
        <div class="col">{{task.title}}</div>
        <div class="col ">{{task.description}}</div>
        <div class="col">{{task.deadline}}</div>
        <div class="col">{{task.priority}}</div>
        <div class="col">{{task.complete}}</div>
        <div class="col">
          <button class="btn btn-primary btn-floating">
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
        /* deleteme
        fields: {
          title: undefined,
          description: undefined,
          deadline: undefined,
          priority: undefined,
          complete: undefined,
        }*/
      }
    }, 
    props: {
      task: Object
    },
    methods: {
      deleteTask(){
        this.$emit('deleteTask', this.task)
      }
    }
  
  };
  
  </script>
  
  <style scoped>
  
  </style>