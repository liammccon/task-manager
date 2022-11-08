<template>
    <!-- Button trigger modal 
    <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal">
    Launch demo modal
    </button>
    -->
    <button class="btn btn-primary" id="modal-btn" ref="modalBtn" @click="showModal">Open modal</button>

    <!-- Modal -->
    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
            <!--Header-->
        <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
            <button type="button" class="btn-close" @click="hideModal" aria-label="Close"></button>
        </div>
        <!--Body-->
        <div class="modal-body">
            ...
        </div>
        <div class="modal-footer">
            <button type="button" class="btn btn-secondary" @click="hideModal">Close</button>
            <button type="button" class="btn btn-primary">Save changes</button>
        </div>
        </div>
    </div>
    </div>
</template>

<script>
export default {
    props: {

    },
    methods: {
        showModal() {
            //this.$refs.modalBtn.modal()
            $('#exampleModal').modal("show")
        },
        hideModal(){
            $('#exampleModal').modal("hide")
        }
    }
}
</script>