<template>
<div>
  <Header></Header>
  <Card></Card>
  <Footer></Footer>
</div>
</template>

<script>
import Header from "../components/Header.vue"
import Card from "../components/Card.vue"
import Footer from "../components/Footer.vue"

export default {
    name: "HomePage",
    components: {
        Header,
        Card,
        Footer,
    },
    
}
</script>

<style>

</style>