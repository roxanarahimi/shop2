<template>
  <div class="cover d-none">


    <div class="row justify-content-center">
      <dic class="col-11 col-lg-8 text-center mt-5">
        <img :src="url+'/images/product_24_62da838538419.jpg'" class="img-fluid  " alt="">
      </dic>
    </div>
  </div>
</template>

<script>
import App from '../App'
export default {
  name: "ProductImages",
  components:{App},
  data(){
    return{
      url: App.data().apiUrl,
    }
  }
}
</script>

<style>
.cover{
  position: fixed;
  width: 100%;
height: 100%;
  top:0;
  left: 0;
  background-color: rgba(23, 17, 17, 0.7);
  z-index: 10000;
  overflow: hidden;
}
</style>