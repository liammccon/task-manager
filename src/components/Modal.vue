<template>
    <!--
        This is a modal component that will work to both edit existing tasks and create new ones.
        It takes as input 
            - the task object to edit (can be an empty object for a new task)
            - Whether to edit "EDIT" or create a new "NEW" task
        It returns (with $emit) the edited task object
    -->
    <div class="modal fade" id="newModal"  data-bs-backdrop="static" data-bs-keyboard="false" tabindex="-1" aria-labelledby="newModalLabel" aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered modal-sm">
            <div class="modal-content">
                <!--Header-->
            <div class="modal-header bg-primary text-white">
                <h5 class="modal-title" id="newModalLabel">
                    <i class="fa-solid fa-plus me-2"></i>
                    Add task
                </h5>
            </div>
            <!--Body-->
            <div class="modal-body">
                <div class="container-fluid">

                    <!--Form-->
                    <div class="ltm-label-parent">  
                        <!--Title-->
                        <label class="form-label ltm-label" for="title">Title</label>
                        <input type="text" id="title" placeholder="Enter title" class="form-control ltm-input mb-0" 
                        :class = "(titleInvalid)?'is-invalid':'' "/>
                        <div v-show="titleInvalid" class="ltm-tiny-alert text-danger" >Title is required</div>
                    </div>


                    <div class="mt-4 ltm-label-parent">  
                        <!--Description-->
                        <label class="form-label ltm-label" for="description">Description</label>
                        <input type="text" id="description" placeholder="Enter description" class="form-control ltm-input mb-0"
                        :class = "(descriptionInvalid)?'is-invalid':''"/>
                        <div v-show="descriptionInvalid" class="ltm-tiny-alert text-left text-danger" >Description is required</div>
                    </div>
                    
                    <div class="mt-4 ltm-label-parent">  
                        <!--Deadline-->
                        <label class="form-label ltm-label" for="deadline">Deadline</label>
                        <input type="date" id="deadline" class="form-control ltm-input mb-0 ltm-date-text"
                        :class = "(deadlineInvalid)?'is-invalid':''"/>
                        <div v-show="deadlineInvalid" class="ltm-tiny-alert text-left text-danger" >Deadline is required</div>
                    </div>

                    <!--Priority-->
                    <div class="row mt-4 ltm-label-parent">
                        <label class="form-label ms-2" for="priority" style="text-align:left;">Priority</label>
                        <!--Low-->
                        <div class="col">
                            <input class="form-check-input" type="radio" name="priority" id="priority-low" value="low" checked>
                            <label class="form-check-label" for="priority-low">
                                Low
                            </label>
                        </div>
                        <!--Medium-->
                        <div class="col">
                            <input class="form-check-input" type="radio" name="priority" id="priority-med" value="med">
                            <label class="form-check-label" for="priority-med">
                                Med
                            </label>
                        </div>
                        <!--High-->
                        <div class="col">
                            <input class="form-check-input" type="radio" name="priority" id="priority-high" value="high">
                            <label class="form-check-label" for="priority-high">
                                High
                            </label>
                        </div>
                    </div>
                </div>
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-primary" @click="addTask">
                    <i class="fa-solid fa-plus me-2"></i>
                    Add
                </button>
                <button type="button" class="btn btn-danger" @click="hideModal">
                    <i class="fa-solid fa-trash me-2"></i>
                    Cancel
                </button>
            </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        task: Object,
        type: String
    },
    data(){
        return {
            
        }
    },
    methods: {

    }
    
}
</script>

<style scoped>

</style>