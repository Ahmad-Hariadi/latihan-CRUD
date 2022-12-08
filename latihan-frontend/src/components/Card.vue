<template>
<div>
    <router-link to="/add" class="btn btn-primary mt-3 ml-3" v-show="!success">Add Data</router-link>
    <div class="row mt-3 px-3">
        <div class="col-sm-4 ms-3 mt-3 >" v-show="!success" v-for="item in studentData" :key="item.id">
            <div class="card  border border-secondary rounded"  >
                <div class="card-body" >
                    <h5 class="card-title">{{item.nama + ", "+item.umur+" "+"years old"}}</h5>
                    <p class="card-text">{{item.deskripsi_diri}}</p>
                    <table>
                        <tr>
                            <td>Email</td>
                            <td>:</td>
                            <td>{{item.email}}</td>
                        </tr>
                        <tr>
                            <td>Soft Skills</td>
                            <td>:</td>
                            <td>{{item.soft_skill}}</td>
                        </tr>
                        <tr>
                            <td>Hard Skills</td>
                            <td>:</td>
                            <td>{{item.hard_skill}}</td>
                        </tr>
                        <tr>
                            <td>Interest</td>
                            <td>:</td>
                            <td>{{item.interest}}</td>
                        </tr>
                    </table>

                    <div class="d-flex mt-3">
                        <router-link
                            :to="'/update/' + item.id"
                            class="btn btn-sm btn-primary mr-2"
                            @click="$emit('updateStudentEmit', item)">
                            Update
                        </router-link>
                        <button
                            class="btn btn-sm btn-danger"
                            @click="deleteStudentFunc(item.id)">
                            Delete
                        </button>
                        
                        <img 
                            v-if="item.jenis_kelamin == 'Male'"
                            src="../assets/img/male.png"
                            class="ml-auto"
                            style="min-width: 2vw; height: 5vh;">

                        <img 
                            v-else
                            src="../assets/img/female.png"
                            class="ml-auto"
                            style="min-width: 2vw; height: 5vh;">
                    </div>
                </div>
            </div>
        </div>    
        <SuccessDelete class="col-sm-6 m-auto mt-3" v-show="success"></SuccessDelete>
    </div>
</div>
</template>

<script>
import studentService from "../services/studentService";
import SuccessDelete from "../components/SuccessDelete.vue";
export default {
    name: "CardComponent",
    data: function() {
        return {
            studentData: null,
            success: false,
        }
    },
    components: {
        SuccessDelete,
    },
    methods: {
        getStudent() {
            studentService.getAll()
            .then(response => {
                this.studentData = response.data;
                console.log(this.studentData);
            })
            .catch(e => {
                console.log(e);
            });
        },
        deleteStudentFunc(id) {
            if(confirm("Are you sure want to delete?")) {
                studentService.deleteStudent(id)
                .then(response => {
                    console.log(response.data);
                    this.success = true;
                })
                .catch(e => {
                    console.log(e);
                });
                // location.reload();
            } else {
                alert("Your data is safe!");
            }
        },
    },
    mounted() {
        this.getStudent();
    }
}
</script>

<style>

</style>