<template>
    <Header/>  
    <div class="welcome-message">
        <h3>Welcome back customer!</h3>
    </div>
    <img src="../assets/restologo.png"/>
    <h1>Log In</h1>

    <div class="login">

        <label>Email</label>
        <input type="email" v-model="email" required="Please enter email address." />
        <label>Password</label>
        <input type="password" v-model="password" required="Please enter password!" />

        <button type="button" :onclick="logInFunction">Log In</button>

        <div class="container sign up">
            <p> Not a member?
                <a href="/sign-up">Sign up now.</a>
            </p>
        </div>
    </div>
</template>

<script>
import Header from './Header.vue'
import axios from 'axios'
export default {
    name: 'LoginPage',
    components:{
        Header,
    },

    data(){
        return{
          email:'',
          password:''
        }
    },
    methods:{
     async logInFunction(){
        let result = await axios.get(
            `http://localhost:3000/users?email=${this.email}&pasword=${this.password}`
        )
        
        if(result.status==200 && result.data.length>0){

            localStorage.setItem("user-info",JSON.stringify(result.data[0])),
            this.$router.push({name:'HomePage'})
        }

        console.warn(result)
     }
    },
    mounted (){
        let user = localStorage.getItem('user-info')

        if (user) {
            this.$router.push({ name: 'HomePage' })

        }
    }
}
</script>

<style>

.login input{
    height:40px;
    width:300px;
    padding-left: 20px;
    margin-top: auto;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 20px;
    border: 1px solid #808080;
    border-radius: 8px;
    display: block;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}

.welcome-back h3{
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    font-size: 25px;
}

.login button{
    height: 40px;
    width: 320px;
    color: #ffffff;
    background :#000000;
    cursor:pointer;
    border: 1px solid #808080;
    border-radius: 8px;
    
}

.login label{
    color:#000000;
    font-weight: bold;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}

</style>
