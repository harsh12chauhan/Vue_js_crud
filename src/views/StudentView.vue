import { RouterLink } from 'vue-router';
<template>
    <div>
        <div class="card">
            <div class="card-header">
                <h4>
                    Students
                    <RouterLink to="/students/create" class="btn btn-primary float-end"> 
                        Add Student
                    </RouterLink>
                </h4>
            </div>
            <div class="card-boady">
                <div class="table table-boardered">
                    <thead>
                        <tr>
                            <th>ID</th>
                            <th>Name</th>
                            <th>Email</th>
                            <th>Phone</th>
                            <th>Address</th>
                            <th>Update</th>
                            <th>Delete</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(student,index) in this.students" :key="index">
                            <td>{{ student.id?student.id :'No Data To Display' }}</td>
                            <td>{{ student.name?student.name :'No Data To Display' }}</td>
                            <td>{{ student.email?student.email :'No Data To Display' }}</td>
                            <td>{{ student.phone?student.phone :'No Data To Display' }}</td>
                            <td>{{ student.address?student.address :'No Data To Display' }}</td>
                            <td><RouterLink :to="{ path: '/students/update/' + student.id }"><button class="btn_form green">Update</button></RouterLink></td>                            
                            <td><button class="btn_form red" @click="deleteUser(student.id)">Delete</button></td>
                        </tr>
                    </tbody>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import { RouterLink } from 'vue-router';
import UpdateView from './UpdateView.vue';

const routes = [
  {
    path: '/students/update/:id',
    component: UpdateView,
  },
  // Other routes
];

export default{
    name: 'students',
    data() {
        return {
            students: []
        };
    },
    mounted() {
        this.getUsers();
    },
    methods: {
        async getUsers() {
            await axios.get('http://localhost:3000/data')
                .then(res => {
                this.students = res.data;
                // console.log(this.students); 
            });
        },
        async deleteUser(id){
            const userConfirmed = window.confirm("Are you sure you want to delete the user?");
            if(userConfirmed){
                await axios.delete(`http://localhost:3000/data/${id}`)
                .then(res=>{"success"})
                .catch(error=>{error})
                location.reload();
            }else{
                console.log("user not deleted");
            }
        }
    },
    components: { RouterLink }
}
</script>

<style>
 .btn_form{
        color: white;
        border: none;
        padding: 5px 15px 5px 15px ;
        border-radius: 7px;
        margin: 20px 235px 0px 10px;
    }
    .green{
        background-color: green;
    }
    .red{
        background-color: rgba(158, 6, 34, 0.878);
    }
    .btn_form:hover{
        transform: scale(1.1);
        transition: 0.3s ease-in-out;
    }
</style>