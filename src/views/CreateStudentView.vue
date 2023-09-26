<script>
import axios from 'axios'
    export default{
        name:'create_student',
        data(){
            return {
                error:{
                    ename:null,
                    eemail:null,
                    ephone:null,
                    eaddress:null
                },
                formData:{
                    name:'',
                    email:'',
                    phone:'',
                    address:''
                },
                check:true,
            }
        },
        methods:{
            validations(){ 
                this.check = true;
                if(!this.formData.name){
                    this.error.ename = true;
                    this.check = false;
                }                                    
                if(!this.formData.email){
                    this.error.eemail = true;
                    this.check = false;
                }                                    
                if(!this.formData.phone){
                    this.error.ephone = true;
                    this.check = false;
                }                                    
                if(!this.formData.address){
                    this.error.eaddress = true;
                    this.check = false;
                }                                    
                return this.check
            },
           async postUsers() {
               if(this.validations()){
                   await axios.post('http://localhost:3000/data',this.formData)
                   .then(res=>"success")
                   .catch(err=>{err})
                   this.$router.push('/students')
               }
            }
        }
    }
</script>
<template>
   <div class="container">
       <form @submit.prevent="postUsers" class="form_action">
        <h1 class="heading"><u>Create user</u></h1>
        <div class="left_form">
            <div class="div_form">
                <label for="name" class="label_form"> Name </label>
                <input type="text" placeholder="Name" name="name" :class="error.ename && !(formData.name) ?'red_err':'input_form'" v-model="formData.name">
            </div>
            <div class="div_form">
                <label for="email" class="label_form"> Email </label>
                <input type="text" placeholder="Email" name="email" :class="error.eemail && !(formData.email) ?'red_err':'input_form'" v-model="formData.email">
            </div>
        </div>
        <div class="right_form">
            <div class="div_form">
                <label for="phone" class="label_form"> Phone </label>
                <input type="text" placeholder="Phone" name="phone" :class="error.ephone && !(formData.phone) ?'red_err':'input_form'" v-model="formData.phone">
            </div>
            <div class="div_form">
                <label for="address" class="label_form"> Address </label>
                <input type="text" placeholder="Address" name="address" :class="error.eaddress && !(formData.address) ?'red_err':'input_form'" v-model="formData.address">
            </div>
        </div>
        <button class="btn_form blue" type="submit">Create</button>
    </form>
   </div>
</template>

<style>
    .container{
        margin: 50px 40px 0px 40px ;
    }
    .form_action{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
    .heading{
        font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
        font-weight: 500;
        margin-bottom: 15px;
    }
    .label_form{
        font-size: 20px;
        font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
        font-weight: 400;
    }
    .div_form{
        display: flex;
        flex-direction: column;
    }
    .input_form{
        margin: 5px;
        min-width: 300px;
        border: 2px solid black;
        border-radius: 5px;
    }
    .btn_form{
        color: white;
        border: none;
        padding: 5px 15px 5px 15px;
        border-radius: 7px;
        margin: 20px 235px 0px 10px;
    }
    .blue{
        background-color: rgba(38, 38, 231, 0.899);
    }
    .btn_form:hover{
        transform: scale(1.1);
        transition: 0.3s ease-in-out;
    }
    .red_err{
        margin: 5px;
        min-width: 300px;
        border-radius: 5px;
        animation: shake 0.2s ease-in-out 0s 1;
        box-shadow: 0 0 0.5em red;
        border: 1px solid red;
    }
    @keyframes shake {
        0% { margin-left: 0rem; }
        25% { margin-left: 0.5rem; }    
        75% { margin-left: -0.5rem; }
        100% { margin-left: 0rem; }
    }
</style>