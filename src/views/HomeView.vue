<template>
  <div class="home">
    <div class="row ">
      <div class="col-12 mb-3">
        <!--        <div class=" bg-white " style="min-height: 400px; background: url('img/monaghan-12-1354x508.jpg') center top no-repeat; ">-->
        <div class=" " style="min-height: 400px;">
<!--          <carousel :slides="slides"  />-->

          <slider :slides="slides" />
        </div>
      </div>
      <div class="col-12 mb-3">
        <div class="card ">

          <div class="card-body">

            <div class="text-start mb-3">
              <label class="labels fw-bold text-black-50">جدید ترین ها</label>
              <hr class="mb-4" style="margin-top: -2px;color: #dddddd">
            </div>
            <div class="row">
              <div v-for="item in news" :key="item.id" class="col-12 col-sm-6 col-md-4 col-xl-2 mb-3">
                <productCard :product = "item"/>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="col-lg-8  mb-3">
        <div class="card h-100">

          <div class="card-body">
            <div class="text-start">
              <div class="text-start mb-3">
                <label class="labels fw-bold text-black-50">تخفیف ها</label>
                <hr class="mb-4" style="margin-top: -2px;color: #dddddd">
              </div>
              <div class="row">
                <div v-for="item in off" :key="item.id" class="col-12 col-sm-6 col-xl-3 mb-3">
                  <productCard :product = "item"/>
                </div>
              </div>
            </div>

          </div>
        </div>


      </div>
      <div class="col-lg-4  mb-3">
        <div class="card h-100">
          <div class="card-body">
            <div class="text-start">
              <div class="text-start mb-3">
                <label class="labels fw-bold text-black-50">ویژه</label>
                <hr class="mb-4" style="margin-top: -2px;color: #dddddd">
              </div>

              <div class="row">
                <div v-for="item in limited" :key="item.id" class="col-12 col-sm-6 col-lg-12 col-xl-6 mb-3">
                  <productCard :product = "item"/>
                </div>
              </div>
            </div>

          </div>
        </div>


      </div>

      <div class="col-12 mb-3">
        <div class=" bg-white">
          <img src="/img/monaghan-5-1354x508.jpg" class="w-100" alt="">
        </div>
      </div>

      <div class="col-lg-4 mb-3">
        <div class="card h-100">
          <div class="card-body">
            <div class="text-start">
              <div class="text-start mb-3">
                <label class="labels fw-bold text-black-50">محدود شده ها</label>
                <hr class="mb-4" style="margin-top: -2px;color: #dddddd">
              </div>
              <div class="row">
                <div v-for="item in limited" :key="item.id" class="col-12 col-sm-6 col-lg-12 col-xl-6 mb-3">
                  <productCard :product = "item"/>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="col-lg-8 mb-3">
        <div class="card h-100">

          <div class="card-body">
            <div class="text-start">
              <div class="text-start mb-3">
                <label class="labels fw-bold text-black-50">پر فروش ترین ها</label>
                <hr class="mb-4" style="margin-top: -2px;color: #dddddd">
              </div>
              <div class="row">
                <div v-for="item in sale" :key="item.id" class="col-12 col-sm-6 col-xl-3 mb-3">
                  <productCard :product = "item"/>
                </div>
              </div>

            </div>
            <!--            <carousel :transition="1000" :autoplay="0"  :all="sale" :show="3" />-->

          </div>
        </div>
      </div>
      <div class="col-12 mb-3 d-none">
        <div class="card">
          <div class="card-body">
            <div class="text-start">
              <div class="text-start mb-3">
                <label class="labels fw-bold text-black-50">بزودی...!</label>
                <hr class="mb-4" style="margin-top: -2px;color: #dddddd">
              </div>

            </div>



          </div>
        </div>


      </div>

    </div>

  </div>
</template>

<script>
// @ is an alias to /src

import ProductCard from "@/components/ProductCard";
import Slider from "@/components/Slider";
// import Carousel from "@/components/Carousel";
export default {
  name: 'HomeView',
  components: {Slider, ProductCard},
  data(){
    return{
      slides: [],
      news:[],
      off:[],
      vip:[],
      limited:[],
      sale:[],
      soon:[],

      url:'https://panel.shop2.webagent.ir',
    }
  },
  mounted(){

    this.getSlides();
    this.getOff();
    this.getNew();
    this.getVip();
    this.getLimited();
    this.getSale();

  }
  ,
  methods:{
    getNew(){
      let params = '?stock=&cat_ids=&off=&sort=new&search=&limit=6&sale=false';
      axios.get(this.url+'/api/product'+params) // app.data.apiUrl
          .then((response)=>{ this.news = response.data;})
          .catch((error)=>{console.log(error)});
    },
    getOff(){
      let params = '?stock=&cat_ids=&off=true&sort=&search=&limit=4&sale=false';
      axios.get(this.url+'/api/product'+params) // app.data.apiUrl
          .then((response)=>{ this.off = response.data;})
          .catch((error)=>{console.log(error)});
    },
    getVip(){
      let params = '?stock=true&cat_ids=&off=&sort=&search=&limit=2&sale=false';
      axios.get(this.url+'/api/product'+params) // app.data.apiUrl
          .then((response)=>{ this.vip = response.data;})
          .catch((error)=>{console.log(error)});
    },
    getLimited(){
      let params = '?stock=limited&cat_ids=&off=&sort=&search=&limit=2&sale=false';
      axios.get(this.url+'/api/product'+params) // app.data.apiUrl
          .then((response)=>{ this.limited = response.data;})
          .catch((error)=>{console.log(error)});
    },
    getSale(){
      let params = '?stock=&cat_ids=&off=&sort=&search=&limit=4&sale=true';
      axios.get(this.url+'/api/product'+params) // app.data.apiUrl
          .then((response)=>{ this.sale = response.data;})
          .catch((error)=>{console.log(error)});
    },
    getSoon(){
      let params = '?stock=&cat_ids=&off=&sort=&search=&limit=6&sale=';
      axios.get(this.url+'/api/product'+params) // app.data.apiUrl
          .then((response)=>{ this.soon = response.data;})
          .catch((error)=>{console.log(error)});
    },
    getSlides(){
      axios.get(this.url+'/api/slide')
          .then((response)=>{ this.slides = response.data
          console.log(response.data)
          ;})
          .catch((error)=>{console.log(error)});
    },

  }
}
</script>
<style>
.labels{
  display: inline-block;
  padding-bottom: 5px;
  text-align: right;
  cursor: pointer;
}

</style>
