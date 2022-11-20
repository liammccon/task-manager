<template>
    <!--
        This is a modal component that will work to both edit existing tasks and create new ones.
        It takes as input 
            - the task object to edit (can be an empty object for a new task)
            - Whether to edit "EDIT" or create a new "NEW" task
        It returns (with $emit) the edited task object
    -->
    <div class="modal fade" id="modal"  data-bs-backdrop="static" data-bs-keyboard="false" tabindex="-1" aria-labelledby="modalLabel" aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered modal-sm">
            <div class="modal-content">
                <!--DeleteMe!-->
                

                <!--Header-->
                <div class="modal-header bg-primary text-white">
                    <h5 class="modal-title" id="modalLabel">
                        <span v-if="isEdit()">
                            <i class="fa-solid fa-pen-to-square"></i>
                            Edit task
                        </span>
                        <span v-else-if="isNew()">
                            <i class="fa-solid fa-plus me-2"></i>
                            Add task
                        </span>
                        <span v-else>
                            Invalid type!
                        </span>
                        
                    </h5>
                </div>
                <!--Body-->
                <div class="modal-body">
                    <div class="container-fluid">

                        <!--Form-->
                        <div class="ltm-label-parent">  
                            <!--Title - only for new modals-->
                            <div v-if="isNew()">
                                <label class="form-label ltm-label" for="title">Title</label>
                                <input type="text" id="title" placeholder="Enter title" class="form-control ltm-input mb-0" 
                                :class = "(titleInvalid)?'is-invalid':'' "/>
                                <div v-show="titleInvalid" class="ltm-tiny-alert text-danger" >Title is required</div>
                            </div>
                            
                        </div>


                        <div class="mt-4 ltm-label-parent">  
                            <!--Description-->
                            <label class="form-label ltm-label" for="description">Description</label>
                            <input type="text" id="description" placeholder="Enter description" class="form-control ltm-input mb-0"
                            :class = "(descriptionInvalid)?'is-invalid':''" />
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
                                <input class="form-check-input" type="radio" name="priority" id="priority-low" value="low">
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
                    <!--New add button-->
                    <div v-show="isNew()">
                        <button type="button" class="btn btn-primary" @click="addTask">
                            <i class="fa-solid fa-plus me-2"></i>
                            Add 
                        </button>
                    </div>
                    <div v-show="isEdit()">
                        <button type="button" class="btn btn-primary" @click="editTask">
                            <i class="fa-solid fa-pen-to-square me-2"></i>
                            Edit
                        </button>
                    </div>
                    <button type="button" class="btn btn-danger" @click="cancel">
                        <i class="fa-solid fa-ban me2"></i>
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
        type: String //Will either be "EDIT" or "NEW"
    },
    data(){
        return {
            titleInvalid: false,
            descriptionInvalid: false,
            deadlineInvalid: false,
            taskCopy: Object
        }
    },
    methods: {
        showModal() {
            $('#modal').modal({backdrop: 'static', keyboard: false})  //Must press cancel too close modal
            $('#modal').modal("show")
            this.taskCopy = jQuery.extend({}, this.task)
            if(this.isEdit()){
                $("input[name=priority][value=" + this.task.priority + "]").prop('checked', true);
                $("#description").val(this.taskCopy.description)
                $("#deadline").val(this.taskCopy.deadline)
            } else if (this.isNew()){
                var value = 'low';
                $("input[name=priority][value=" + value + "]").prop('checked', true);
            }
            console.log(this.task)
        },
        cancel(){
            this.hideModal()
            if (this.type == "NEW")
                this.clearModalFields()
        },
        hideModal(){
            $('#modal').modal("hide")
        },
        clearModalFields(){
            $(".ltm-input").val("")
            var value = 'low';
            $("input[name=priority][value=" + value + "]").prop('checked', true);
            this.titleInvalid = false
            this.descriptionInvalid = false
            this.deadlineInvalid = false
        },
        isEdit(){
            return this.type=="EDIT"
        },
        isNew(){
           return this.type=="NEW" 
        },
        addTask(){
            if (!this.validate()) {
                console.log("Invalid!")
                return
            }
            //if valid, emit the new task object
            const newTask = this.createTaskFromFields()
            this.$emit('addTask', newTask)
            this.cancel()
        },
        editTask(){
            if (!this.validate()) {
                console.log("Invalid!")
                return
            }
            //if valid, emit the new task object
            const editedTask = this.createTaskFromFields()
            this.$emit('updateTask', editedTask)
            this.hideModal()
        }, validate(){
            
            if (this.isEdit())
                this.titleInvalid = false
            else if (this.isNew())
                this.titleInvalid = $("#title").val()? false : true
            this.descriptionInvalid = $("#description").val()? false : true
            this.deadlineInvalid = $("#deadline").val()? false : true
            
            return !this.titleInvalid && !this.descriptionInvalid && !this.deadlineInvalid
        },
        createTaskFromFields(){
            return  {
                id : this.task.id,
                title: $("#title").val(),
                description: $("#description").val(),
                deadline: $("#deadline").val(),
                priority: $('input[name="priority"]:checked').val(),
                complete: false,
            }
        }
    }
    
}
</script>

<style scoped>
    .ltm-tiny-alert {
        margin-top: 2px;
        margin-left: 5px;
        font-size: 0.8em;
        text-align:left;
    }

    .ltm-label-parent{
        position:relative;
    }
    .ltm-label{
        font-size: .8em;
        background-color: white;
        position: absolute;
        top: -12px;
        left: 10px;
        padding: 0;
        border-radius: 3px;
    }

</style>