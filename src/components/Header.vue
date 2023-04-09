<template>
  <div class="navbar-menu">
    <a href="/"><i class="fa fa-fw fa-home "></i>Home</a>
    <a href="/add-hotel"><i class="fa fa-fw fa-plus-square "></i>Add Hotel</a>
    <a v-on:click="logoutFunction" href="#"><i class="fa fa-fw fa-sign-out"></i>Log Out</a>

  </div>
</template>
<script>

export default {

  name: "Header",
  methods: {
    logoutFunction() {

      console.warn('log out')
      localStorage.clear(),
        this.$router.push({ name: 'LoginPage' })
    }
  }

}
</script>

<style>
i {
  color: #f5deb3;
  text-shadow: 2px 2px 4px grey;
  font-size: 2px;
  padding-top: 5px;
}

.navbar-menu {
  height: 90px;
  background-color: #000000;
  overflow: auto;
}

.navbar-menu a {
  color: #f5f5f5;
  padding: 16px 14px;
  margin-top: 20px;
  margin-bottom: 10px;
  margin-right: 5px;
  float: left;
  justify-content: end;
  text-decoration: none;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  font-size: 25px;
  text-align: center;
  display: flex;
  flex: end;
}

.navbar-menu a:hover {
  background: rgb(85, 35, 35);
  color: whitesmoke;
  border-radius: 4px;
  height: 60px;
}

/*
 Responsive nav-bar menu 
  */
@media screen and (max-width:900px) {
  .navbar-menu a {
    float: none;
    display: block;
  }
}</style>