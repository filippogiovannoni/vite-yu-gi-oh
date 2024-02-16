<script>
export default {
    name: 'LoaderIcon'
}
</script>
<template>
    <div class="loader">
        Loading Cards...
        <i class="fa-solid fa-spinner fa-spin"></i>
    </div>
</template>


<style scoped>
.loader {
    height: 90vh;
    display: flex;
    justify-content: center;
    align-items: center;

    & i {
        padding: 0 0.5rem;
    }
}
</style>