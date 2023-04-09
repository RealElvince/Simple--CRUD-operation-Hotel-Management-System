<template>
    <Header />
    <h1>Welcome to Add Hotel Page</h1>
    <form class="addhotel">
            <label class="label-style">Hotel Name</label>
            <input type="text" name="name" placeholder="Enter hotel name" v-model="hotel.name" />
            <label class="label-style">Contact</label>
            <input type="text" name="contact" placeholder="Enter contact" v-model="hotel.contact" />
            <label class="label-style">Hotel Address</label>
                <input type="text" name="address" placeholder="Enter hotel address" v-model="hotel.address" />

            <button type="button" v-on:click="addHotel" class="btn btn-dark">Add new Hotel</button>
    </form>
</template>

<script>
import Header from './Header.vue'
import axios from 'axios'
export default {
    name: "AddHotel",

    data(){
        return{
          hotel:{
            name:'',
            contact:'',
            address:'' 
          }
        }
    },
    methods:{
      async addHotel(){
        console.warn(this.hotel);
        const result=await axios.post("http://localhost:3000/hotel",{
            name:this.hotel.name,
            contact:this.hotel.contact,
            address:this.hotel.address,
       
        
        });
       if (result.status==201){
        this.$router.push({name:'HomePage'});
    }
        console.warn("result:",result);

      }
    },
    components: {
        Header,
    },


    mounted() {
        let user = localStorage.getItem('user-info')

        if (user) {
            this.$router.push({ name: 'HomePage' })

        }
    }
}
</script>

<style>
.label-style{
    font-weight: bold;
    font-size: 18px;
} 
 .addhotel input{
   height:60px;
    width:500px;
    padding-left: 20px;
    padding-top: 10px;
    margin-top: auto;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 20px;
    border: 1px solid #808080;
    border-radius: 8px;
    display: block;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
} 
.btn-dark{
    height: 60px;
    width: 500px;
    color: #ffffff;
    border-radius: 8px;
    cursor: pointer;
    justify-content: end;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}
</style>