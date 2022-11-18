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
                {{type}}
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
        showModal() {
            $('#modal').modal({backdrop: 'static', keyboard: false})  //Must press cancel too close modal
            $('#modal').modal("show")
        }
    }
    
}
</script>

<style scoped>

</style>