<template>
  <Header />
  <h2 class="h2-content">Hello <span class="span-content">{{ name }}</span>,welcome to our main page</h2>
  <table class="table table-striped table-dark">
    <thead class="table-head">
      <tr >
        <th scope="col">id</th>
        <th scope="col">Hotel name</th>
        <th scope="col">Contact</th>
        <th scope="col">Address</th>
        <th scope="col">Actions</th>
      </tr>
    </thead>
    <tbody>

      <tr v-for="item in hotel" :key="item.id">
        <th scope="row">{{ item.id }}</th>
        <td>{{ item.name }}</td>
        <td>{{ item.contact }}</td>
        <td>{{ item.address }}</td>
        <td>
          <router-link :to="/update-hotel/+item.id">Update</router-link>
          <button type="button" v-on:click="deleteHotel(item.id)" class="btn btn-danger">Delete</button>
        
        </td>
        
      </tr>
    </tbody> 
  </table>   
</template>

<script>
import Header from './Header.vue'
import axios from 'axios';
export default {
  name: "HomePage",
  data() {
    return {
      name: '',
      hotel: []
    }
  },
  components: {
    Header,
  },

  methods:{
    async deleteHotel(id){

      let result=await axios.delete('http://localhost:3000/hotel/'+id)
    console.warn(id)
    this.loadData();
    },

    async loadData(){
         let user = localStorage.getItem('user-info')
      this.name = JSON.parse(user).name;

      if (!user) {
        this.$router.push({ name: 'SignUp' })

      }

      let result = await axios.get("http://localhost:3000/hotel");
      console.warn(result);
      this.hotel = result.data;


    }
  },

  async mounted() {
    
    this.loadData()

  }
}
</script>

<style>
.btn-danger{
  size: 20px;
  padding-left: 10px;
}
.table-head{
  font-weight: bold;
  font-size: 18px;
}
.table-striped{
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif ;
  height: 40px;
  width: 45cm;
  margin-left: 20px;
  margin-right: 10px;
  margin-bottom: 5px;
  display: center;
  border-radius: 5px;
}

.h2-content {
  flex: start;

}

.span-content {
  color: #a52a2a;
}
</style>