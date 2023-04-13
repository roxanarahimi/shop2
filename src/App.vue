<template>

  <header >
    <div class="col-12 bg-2">
      <div class="">
        <img src="img/600x60-safir-code.gif" width="100%" alt="">
        <div class="px-5" style="width: 100%; height: 150px; ">


          <div style="float: none; padding-top: 30px; cursor: pointer">
          <a href="/">
            <img width="150px" src="img/roxi2.png" alt="">
          </a>
          </div>

        </div>
      </div>
    </div>
  </header>
  <div class="bg-white p-0 mb-3 row mx-0">
    <div  class="col-sm-4 col-md-3 text-start">
      <input v-if="this.$route.name == 'products'" type="text" id = "search"  placeholder = "جستوجوی محصول..." class=" mt-3 form-control form-control-sm">
      <router-link v-else to="/products"  class="btn btn-sm btn-dark mt-3 mb-2">جستوجوی محصول</router-link>
    </div>
   <nav class="col-sm-8 col-md-9 d-flex justify-content-end py-3">
     <router-link id="home" to="/" >خانه </router-link>
     <router-link id="products" to="/products" >محصولات </router-link>
     <router-link id="profile" class="d-none" to="/profile" >پروفایل </router-link>
     <router-link id="cart" class="d-none" to="/cart" >سبد خرید </router-link>
     <router-link id="login" to="/login" >ورود </router-link>
     <a  id="logout" class="d-none" @click="logout"  >خروج</a>
   </nav>
    <!--    <router-link to="/">Home</router-link> |-->
    <!--    <router-link to="/about">About</router-link>-->
  </div>
  <main class="mx-auto px-3 px-xl-0" style="min-height: 310px">
    <!--    <div class="card p-0 mb-3">-->
    <!--      <div class="card-body">-->
    <!--        <div class="row">-->
    <!--          <div class="col-3">-->
    <!--            <input type="text" placeholder="search..." class="form-control form-control-sm">-->
    <!--          </div>-->
    <!--        </div>-->
    <!--      </div>-->
    <!--    </div>-->
    <!--    <div class="card mb-3">-->
    <!--      <div class="card-body" style="min-height: 500px">-->
    <router-view/>
    <!--      </div>-->
    <!--    </div>-->
  </main>

  <the-footer />
</template>
<script>
import TheFooter from '@/components/TheFooter'
import Products from "@/views/Products";
import login from "@/views/Login";
export default {
  components: {TheFooter, Products},

  data(){
    return{
      apiUrl:'https://panel.webagent.ir',
      imgUrl:'https://panel.webagent.ir',
    }
  },
  updated() {
        let user = JSON.parse(localStorage.getItem('user'))
    if(!user){
      document.getElementById('login').classList.remove('d-none')
      document.getElementById('cart').classList.add('d-none')
      document.getElementById('profile').classList.add('d-none')
      document.getElementById('logout').classList.add('d-none')
    }else{
      document.getElementById('login').classList.add('d-none')
      document.getElementById('cart').classList.remove('d-none')
      document.getElementById('profile').classList.remove('d-none')
      document.getElementById('logout').classList.remove('d-none')
    }
  },
  setup(){
    const logout = ()=>{
      localStorage.clear();
      document.getElementById('login').classList.remove('d-none')
      document.getElementById('cart').classList.add('d-none')
      document.getElementById('profile').classList.add('d-none')
      document.getElementById('logout').classList.add('d-none')
    }

    return{
      logout,
    }
  }
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a:not(.btn) {
  font-weight: bold;
  /*color: #2c3e50;*/
  margin-right: 15px;
  margin-left: 15px;
  color: #a8a8a8;
  text-decoration: none;
}

body {
  /*background-color: #91e7bf;*/
  max-width: 1000px;
}
.card{
  overflow: hidden;
}
a{
  text-decoration: none;
}
#logout{
  cursor: pointer;
}
</style>
