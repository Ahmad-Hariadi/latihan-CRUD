<template>
<div>
  <Header></Header>
  <Form
    :updateStudentProps = "studentData"></Form>
  <Footer></Footer>
</div>
</template>

<script>
import Header from "../components/Header.vue"
import Form from "../components/Form.vue"
import Footer from "../components/Footer.vue"
import studentService from '@/services/studentService'
export default {
    name: "UpdatePage",
    components: {
        Header,
        Form,
        Footer,
    },
    methods: {
      updateData() {
        let id = this.$route.params.id;

        studentService.updateGetId(id)
        .then(Response => {
            this.studentData = Response.data;
            console.log(Response.data);
        })
        .catch(e => {
            console.log(e);
        })
      }
    },
    mounted() {
        this.updateData();
    },
    data(){
      return {
        studentData: null,
      }
    }
}
</script>


<style>

</style>