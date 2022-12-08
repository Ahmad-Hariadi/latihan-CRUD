<template>
    <div class="card-body border border-secondary">
        <h5 class="card-title">Success!</h5>
        <p class="card-text">Student data has been deleted!</p>
        <router-link to="/add" class="btn btn-primary text-white">Close</router-link>
    </div>
</template>

<script>
export default {
    name: "SuccessDeleteComponent",
}
</script>

<style>

</style>