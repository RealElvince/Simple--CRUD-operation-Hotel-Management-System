<template>
    <Header/>
    <img src="../assets/restologo.png"/>
    <h1>Sign Up</h1>
    <div class="register">
        <label>Name</label>
       <input type="text" v-model="name"  required="Please enter name." />
       <label>Email</label>
        <input type="email"  v-model="email"  required="Please enter email address."/>
        <label>Password</label>
       <input type="password" v-model="password" required="Please enter password!"/>
       <label>Confirm password</label>
        <input type="password" v-model="password2" required/>
       <button type="button" :onclick="signUpFunction">Sign Up</button>

       <div  class="container login">
         <p> Already have an account? 
            <a href="/log-in">Log In.</a></p>
       </div>
      
    </div>
</template>

<script>
   import Header from './Header.vue'
   import axios from 'axios'
   export default{
    name:'SignUp',
    components:{
        Header
    },
    data(){
        return{
            name:'',
            email:'',
            password:'',
            password2:''
        }

    },
    methods:{
      async signUpFunction (){
        let result= await axios.post("http://localhost:3000/users",{
          name:this.name,
          email:this.email,
          password:this.password,
          password2:this.password2
        });

        console.warn(result);
        if(result.status==201){
            
            localStorage.setItem("user-info",JSON.stringify(result.data))
             this.$router.push({ name: 'HomePage' })

            
        }
     }
    },
    mounted(){
        let user=localStorage.getItem('user-info')

        if(user){
            this.$router.push({name:'HomePage'})
            
        }
    }
   }
</script>

<style>
.register input{
 height: 40px;
 width: 300px;
 display: block;
 padding-left: 20px;
 margin-left: auto;
 margin-bottom: 20px;
 margin-right: auto;
 border: 1px solid grey;
 border-radius: 8px;
 align-content: flex-start;
}
.register button{
    height: 40px;
    width: 320px;
    border: 1px solid grey;
    color: #ffffff;
    background: #000000;
    border-radius: 8px;
    cursor: pointer;
}
.register label{
    color: #000000;
    align-content: flex-start;
    font-weight:bold ;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}
</style>