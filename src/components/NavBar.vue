<template>
    <div class="container-fluid bg-primary text-white m-0 mb-4 p-2">
      <div class="row ltm-content">
        <div class="col"></div>
        <!--Title-->
        <div class="col-6">
          <div class="container-fluid h3 pt-1">
            <i class="fa-solid fa-list-check me-2"></i>
            Task Manager
          </div>
        </div>
  
        <!--button area-->
        <div class="col">
          <div class="container-fluid">
            <button
              class="btn text-white ltm-add-btn"
              style="background-color: #55acee"
              @click="addBtnClick"
            >
              <i class="fa-solid fa-plus me-2"></i>
              Add
            </button>
          </div>
        </div>
      </div>
    </div>
</template>
  
<script>
export default {
  name: 'NavBar',
  data () {
    return { }
  }, 
  methods: {
    addBtnClick(){
      this.$emit("addBtnClicked")
    }
  }
};
</script>

<style scoped>
.ltm-nav-bar {
  margin-bottom: 20px;
}
.ltm-center {
  text-align: center;
}
.ltm-add-btn {
  min-width: 100px;
}
.ltm-content{
  /* Will let the content be smaller than the main page width, up to 350px */
  width: 100vw;
  min-width: 350px;
}
</style>
  