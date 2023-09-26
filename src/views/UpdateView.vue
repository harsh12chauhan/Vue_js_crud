<script>
import axios from 'axios'
    export default{
        data(){
            return {
                formData:{
                    name:'',
                    email:'',
                    phone:'',
                    address:''
                }
            }
        },
        mounted(){
            this.getSingleuser(this.$route.params.id);
        },
        methods:{
           async getSingleuser(id){
                await axios.get(`http://localhost:3000/data/${id}`)
                    .then(res => {
                        this.formData = res.data;
                        console.log(res.data);
                }).catch(err=>{err});
             },
             async updateUser(id){
                console.log(this.formData);
                await axios.patch(`http://localhost:3000/data/${id}`,this.formData)
                .then(res=>{"success"},this.formData)
                .catch(err=>{err})
                this.$router.push('/students')
             }
        }
    }
</script>
<template>
   <div class="container">
       <form class="form_action">
        <h1 class="heading"><u>Update user</u></h1>
        <div class="left_form">
            <div class="div_form">
                <label for="name" class="label_form"> Name </label>
                <input type="text" placeholder="Name" name="name" class="input_form" v-model="formData.name" >
            </div>
            <div class="div_form">
                <label for="email" class="label_form"> Email </label>
                <input type="text" placeholder="email"  name="email" class="input_form" v-model="formData.email" >
            </div>
        </div>
        <div class="right_form">
            <div class="div_form">
                <label for="phone" class="label_form"> Phone </label>
                <input type="text" placeholder="Phone" name="phone" class="input_form" v-model="formData.phone">
            </div>
            <div class="div_form">
                <label for="address" class="label_form"> Address </label>
                <input type="text" placeholder="Address" name="address" class="input_form" v-model="formData.address">
            </div>
        </div>
        <button class="btn_form blue" @click.prevent="updateUser(formData.id)">Update</button>
    </form>
   </div>
</template>
