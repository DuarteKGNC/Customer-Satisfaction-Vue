<template>
    <div class="container-fluid p-3">
        <div class="header text-center">
            <h1>Tech Support Metrics</h1>
        </div>
        <UploaderComp />
    </div>
</template>
<script>
import UploaderComp from '../components/UploaderComp';
export default {
    name: 'DashboardView',
    components: {
        UploaderComp
    }
}
</script>
<style scoped></style>