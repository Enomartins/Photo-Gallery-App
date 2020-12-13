<template>
    <!-- Modal -->
    <div id="myModal" class="modal fade" role="dialog" style="justify-content: center">
        <div class="modal-dialog">

            <!-- Modal content-->
            <div class="modal-content" style="align-text: center">
                <h2>Title</h2>
                <p>this is a sample text</p>
                <div class="modal-body">
                    <img width="100%" style="max-width:350px" class="rounded center" :src="imageURLm" alt="" srcset="">
                </div>
            
            </div>

        </div>
    </div>
</template>

<script>

export default {
    name: 'Modal',

    props: ["imageURL"],

    data () {
        return {
            imageURLm: ''
        }
    },

    mounted() {
        this.imageURLm = this.imageURL
    }
}
</script>