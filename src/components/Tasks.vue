<template>
    <!--Header-->
    <div class="container-fluid">
      <div class="row">
        <div class="col text-muted">Title</div>
        <div class="col text-muted">Description</div>
        <div class="col text-muted">Deadline</div>
        <div class="col text-muted">Priority</div>
        <div class="col text-muted">Complete</div>
        <div class="col text-muted">Action</div>
        <div class="me-2">
          <hr />
        </div>
      </div>
    </div>
  
    <div v-for="task in taskList">
      <Task :task="task" @deleteTask="deleteTask"/>
    </div>
  
  </template>
  
  <script>
  import Task from './Task.vue'
  
  export default {
    name: 'Tasks',
    components: {
      Task
    },
    props: {
      taskList: Object,
    }, 
    emits: ["deleteTask"],

    data() {
      return {
        nextID: 1, //A unique ID assigned to each task for easier retrieval / editing
      };
    },
    methods: {
    deleteTask (task){
      this.$emit("deleteTask", task.id)
    }
    }
  };
  </script>
  