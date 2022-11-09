<template>
    <!-- Button trigger modal 
    <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal">
    Launch demo modal
    </button>
    -->
    <button class="btn btn-primary" id="modal-btn" ref="modalBtn" @click="showModal">Open modal</button>

    <!-- Modal -->
    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog modal-dialog-centered modal-sm">
        <div class="modal-content">
            <!--Header-->
        <div class="modal-header bg-primary text-white">
            <h5 class="modal-title" id="exampleModalLabel">
                <i class="fa-solid fa-plus me-2"></i>
                Add task
            </h5>
        </div>
        <!--Body-->
        <div class="modal-body">
            <div class="container-fluid">

                <!--Form-->
                <div class="">  
                    <!--Title-->
                    <input type="text" id="title" placeholder="Enter title" class="form-control ltm-input mb-0" 
                    :class = "(titleInvalid)?'is-invalid':''"/>
                    <label class="form-label ltm-label" for="title" hidden>Title</label>
                    <div v-show="titleInvalid" class="ltm-tiny-alert text-danger" >Title is required</div>
                </div>


                <div class="mt-4">  
                    <!--Desceription-->
                    <input type="text" id="description" placeholder="Enter description" class="form-control ltm-input mb-0"
                    :class = "(descriptionInvalid)?'is-invalid':''"/>
                    <label class="form-label ltm-label" for="description" hidden>Description</label>
                    <div v-show="descriptionInvalid" class="ltm-tiny-alert text-left text-danger" >Description is required</div>
                </div>
                
                <div class="mt-4">  
                    <!--Deadline-->
                    <input type="date" id="deadline" class="form-control ltm-input mb-0"
                    :class = "(deadlineInvalid)?'is-invalid':''"/>
                    <label class="form-label ltm-label" for="deadline" hidden>Deadline</label>
                    <div v-show="deadlineInvalid" class="ltm-tiny-alert text-left text-danger" >Deadline is required</div>
                </div>

                <!--Priority-->
                <div class="row mt-4">
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

    },
    data(){
        return {
            titleInvalid: false,
            descriptionInvalid: false,
            deadlineInvalid: false,
        }
    },
    methods: {
        showModal() {
            $('#exampleModal').modal("show")
        },
        hideModal(){
            $('#exampleModal').modal("hide")
            this.clearModal()
        },
        addTask(){
            this.validate()
            if (this.titleInvalid || this.descriptionInvalid || this.dateInvalid) {
                //alert("INVALID")
            }
        }, validate(){
            const needsVal = [$("#title"), $("#description"), $("#deadline")]
            
            this.titleInvalid = $("#title").val()? false : true
            this.descriptionInvalid = $("#description").val()? false : true
            this.deadlineInvalid = $("#deadline").val()? false : true
            
            return needsVal.every(i=> i.val())
        },

        /**
         * Clears all inputs and invalidity
         */
        clearModal(){
            $(".ltm-input").val("")
            var value = 'low';
            $("input[name=priority][value=" + value + "]").prop('checked', true);
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
</style>