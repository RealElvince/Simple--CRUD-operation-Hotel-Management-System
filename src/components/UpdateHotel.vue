<template>
 <Header/>
 <h1>Welcome to update Hotel page.</h1>
 <form class="updatehotel">
                <label class="label-style">Hotel Name</label>
                <input type="text" name="name" placeholder="Enter hotel name" v-model="hotel.name" />
                <label class="label-style">Contact</label>
                <input type="text" name="contact" placeholder="Enter contact" v-model="hotel.contact" />
                <label class="label-style">Hotel Address</label>
                    <input type="text" name="address" placeholder="Enter hotel address" v-model="hotel.address" />

                <button type="button" v-on:click="updateHotel" class="btn btn-dark">Update Hotel</button>
        </form>
</template>

<script>

import Header from './Header.vue'
import axios from 'axios'
export default{
    name:"UpdateHotel",
    data() {
        return {
            hotel: {
                name: '',
                contact: '',
                address: ''
            }
        }
    },
    methods:{
     async updateHotel(){
        console.warn(this.hotel);
            const result = await axios.put("http://localhost:3000/hotel"+this.$route.params.id, {
                name: this.hotel.name,
                contact: this.hotel.contact,
                address: this.hotel.address,


            });
            if (result.status == 200) {
                this.$router.push({ name: 'HomePage' });
            }
            console.warn("result:", result);
     }
    },
    components:{
        Header,
    },

    async  mounted() {
        let user = localStorage.getItem('user-info')

        if (!user) {
            this.$router.push({ name: 'HomePage' })

        }
        console.warn(this.$route.params.id);

        const result= await axios.get('http://localhost:3000/hotel/'+this.$route.params.id);

        console.warn(result.data);

        this.hotel=result.data;
    }
}
</script>
<style>
.label-style {
    font-weight: bold;
    font-size: 18px;
}

.updatehotel input {
    height: 60px;
    width: 500px;
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

.btn-dark {
    height: 60px;
    width: 500px;
    color: #ffffff;
    border-radius: 8px;
    cursor: pointer;
    justify-content: end;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}
</style>