<template>
  <div class="card-body border-color border border-secondary">
    <h5 class="card-title">Success!</h5>
    <p class="card-text">Student data has been {{textVal}}!</p>
    <router-link to="/" class="btn btn-primary text-white">Close</router-link>
  </div>
</template>

<script>
export default {
    name: "SuccessFormComponent",
    data: function() {
      return {
        textVal : null,
        currentPath : null,
      }
    },
    mounted() {
      this.currentPath = this.$route.path;
      this.textAlert();
    },
    methods : {
      textAlert() {
        if(this.currentPath == "/add") {
          this.textVal = "inputed";
        } else {
          this.textVal = "updated";
        }
      }
    }
};
</script>

<style scoped>
/* .border-color {
  border: 1px solid rgba(0,0,0,0.4);
} */
</style>
