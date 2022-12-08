<template>
<div>
    <router-link 
        to="/"
        class="btn btn-primary font-weight-bold ml-3 mt-3"
        v-show="!success">
        Back
    </router-link>
  <main class="container-fluid mt-5 mb-5" style="width: 70vw; height: 100vh">
    <form @submit.prevent="submitData" v-show="!success" class="p-4 rounded border border-primary">
      <center>
        <h2 class="mt-4 mb-5">{{titleValue}}</h2>
      </center>
      <div class="form-row p-1">
        <div class="form-group col-md-6">
          <label>Student Name</label>
          <input
            v-model="studentData.nama"
            type="text"
            class="form-control"
            placeholder="Enter name"
            required
          />
        </div>
        <div class="form-group col-md-6">
          <label>Soft Skills</label>
          <input
            v-model="studentData.soft_skill"
            type="text"
            class="form-control"
            placeholder="Enter soft skills"
            required
          />
        </div>
      </div>
      <div class="form-row p-1">
        <div class="form-group col-md-3">
          <label>Student Age</label>
          <input
            v-model="studentData.umur"
            type="text"
            class="form-control"
            placeholder="Enter age"
            required
          />
        </div>
        <div class="form-group col-md-3">
          <label>Gender</label>
          <select class="form-control" 
          v-model="studentData.jenis_kelamin"
          value=""
          required>
            <option value=""></option>
            <option value="Male">Male</option>
            <option value="Female">Female</option>
            
          </select>
        </div>
        <div class="form-group col-md-6">
          <label>Hard Skills</label>
          <input
            v-model="studentData.hard_skill"
            type="text"
            class="form-control"
            placeholder="Enter hard skills"
            required
          />
        </div>
      </div>
      <div class="form-row p-1">
        <div class="form-group col-md-6">
          <label>Student Email</label>
          <input
            v-model="studentData.email"
            type="email"
            class="form-control"
            placeholder="Enter email"
            required
          />
        </div>
        <div class="form-group col-md-6">
          <label>Interest</label>
          <select class="form-control" 
          v-model="studentData.interest"
          value=""
          required>
            <option value=""></option>
            <option value="Data Science">Data Science</option>
            <option value="Network">Network</option>
            <option value="Web Frontend">Web Frontend</option>
            <option value="Web Backend">Web Backend</option>
            <option value="Mobile Apps">Mobile Apps</option>
          </select>
        </div>
      </div>
      <div class="form-group col-md-12 p-1">
        <label>Self Description</label>
        <textarea
          v-model="studentData.deskripsi_diri"
          class="form-control"
          required
          cols="20"
          rows="5"
        ></textarea>
      </div>
      <button 
        type="submit" 
        class="btn btn-primary">
        {{buttonValue}}
      </button>
    </form>
    <SuccessForm v-show="success"></SuccessForm>
  </main>
</div>
</template>

<script>
import studentService from "../services/studentService.js";
import SuccessForm from "../components/SuccessForm.vue";

export default {
    name: "FormComponent",
    data: function() {
      return {
        studentData: {
          "deskripsi_diri" : null,
          "email" : null,
          "hard_skill" : null,
          "interest" : null,
          "jenis_kelamin" : null,
          "nama" : null,
          "soft_skill" : null,
          "umur" : null
        },
        success: false,
        buttonValue: "Submit",
        titleValue: "Add Student"
      }
    },
    methods: {
      submitData: function() {
        let data = this.studentData;
        if(this.buttonValue == "Submit") {
          studentService.insert(data)
            .then(response => {
              console.log(response.data);
              this.success = true;
            })
            .catch(e => {
              console.log(e);
            });
        } else {
          studentService.updateStudent(data.id, data)
            .then(response => {
              this.studentData = response.data;
              this.success = true;
            })
            .catch(e => {
              console.log(e);
            });
        }
      }
    },
    components: {
      SuccessForm,
    },
    props: ["updateStudentProps"],
    watch: {
      'updateStudentProps'(newValue) {
        this.studentData = newValue;
        this.buttonValue = "Update";
        this.titleValue = "Update Student";
      },
  },
}
</script>

<style>

</style>