<template>
    <div class="text-center">
        <div class="row position-relative mt-5">
            <div class="col-12 mt-5">
                <h3>Upload your metrics file here</h3>
                <br>
                <UploadButton />
            </div>
        </div>
    </div>
</template>
<script>
import UploadButton from './UploadButton.vue';
export default {
    name: 'UploaderComp',
    components: {
        UploadButton
    }
}
</script>
<style scoped></style>