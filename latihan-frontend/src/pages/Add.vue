<template>
<div>
    <Header></Header> 
    <Form></Form>
    <Footer></Footer>
</div>
</template>

<script>
import Header from "../components/Header.vue"
import Form from "../components/Form.vue"
import Footer from "../components/Footer.vue"

export default {
    name: "AddPage",
    components: {
        Header,
        Form,
        Footer,
    },
}
</script>

<style>

</style>