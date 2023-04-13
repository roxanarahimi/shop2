<template>
  <router-link :to = "'/product/'+product.id">
    <div class = "card product-card h-100" :class="{'border-light' :this.$route.path=='/', 'border-0' : this.$route.path !== '/'}">
      <img class="sold mx-auto" :src = "url+'/images/sold.png'" v-if="product.stock == 0" alt = "soldout">
      <span class="badge bg-danger mx-1" style="position: absolute;top:5px; left:5px;"  v-if = "product.off != 0">{{ product.off }}%</span>
      <img class="img-fluid" :src="url+product.images[0]" :class="{'img-gray': product.stock == 0}" />

      <div class = "card-body">
        <p class = "card-title fw-bold text-dark">{{ product.title }}</p>
<!--        <small class = "card-subtitle text-muted d-block mb-3">{{ product.subTitle }}</small>-->
        <small class = "card-text text-muted fw-bold d-block me-2" id = "offPrice"  v-if="product.stock != 0">
          {{ product.price - (product.price * parseInt(product.off)/100)}}
          تومان
        </small>
        <small class = "card-text text-muted d-block text-decoration-line-through" v-if = "product.off != 0 && product.stock != 0">
          {{ product.price}}
        </small>
        <small v-else>&nbsp</small>
<!--        <p class="card-text text-muted  d-inline me-2" v-if="product.stock == 0"> </p>-->

        <div class=" mt-0 ">
          <p class="text-muted fw-lighter mb-0 py-0" v-if="product.stock == 0" style="margin-top: -6px">تمام شد</p>
<!--          <p class="fw-lighter my-0" v-else>&nbsp</p>-->
<!--                              <button class="d-inline-block btn btn-success btn-sm fw-lighter my-0" v-else>افزودن به سبد خرید</button>-->
          <small class="flex-row-reverse d-flex justify-content-start mt-1" :title="product.score_count > 0 ? product.score+' ('+product.score_count+' رای)': ''">
            <i class="bi me-1" :class = "{'bi-star-fill': product.score >= 1, 'bi-star' : product.score == 0,'text-warning': product.stock, 'bi-star-half ': 0 < product.score && product.score < 1 ,'text-muted': product.stock == 0}"></i>
            <i class="bi me-1" :class = "{'bi-star-fill': product.score >= 2, 'bi-star' : product.score < 2 && product.score < 1 ,'text-warning': product.stock, 'bi-star-half ': 1 < product.score && product.score < 2 ,'text-muted':product.stock == 0}"></i>
            <i class="bi me-1" :class = "{'bi-star-fill': product.score >= 3, 'bi-star' : product.score < 3 && product.score < 2,'text-warning': product.stock, 'bi-star-half ': 2 < product.score && product.score < 3 ,'text-muted': product.stock == 0}"></i>
            <i class="bi me-1" :class = "{'bi-star-fill': product.score >= 4, 'bi-star' : product.score < 4 && product.score < 3,'text-warning': product.stock, 'bi-star-half ': 3 < product.score && product.score < 4 ,'text-muted': product.stock == 0}"></i>
            <i class="bi me-1" :class = "{'bi-star-fill': product.score >= 5, 'bi-star' : product.score < 5 && product.score < 4,'text-warning': product.stock, 'bi-star-half ': 4 < product.score && product.score < 5 ,'text-muted': product.stock == 0}"></i>
          </small>
        </div>
      </div>
    </div>
  </router-link>
</template>

<script>
import App from "@/App";
export default {
  components: {App},
  props: ['product'],
  name: "ProductCard",
  data(){
    return{
      url: App.data().imgUrl,

    }
  }
}
</script>


<style scoped>
.card:hover {
  box-shadow: 0 0 10px lightgray;
  cursor: pointer;
  transform: scale(1.02);
}
.img-gray{
  filter: grayscale(100%);
}
.sold{
  opacity: 0.6;
  width: 80%;
  position: absolute;
  top: 15px;
  left: 10%;
  z-index: 100;


}
a{
  text-decoration: none;
}
.card-body{
  text-align: start;
}
.border-light{
  border: 1px solid #eeeeee !important;
}
</style>
