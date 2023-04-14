<template>
  <div id="carouselExampleCaptions" class="carousel slide" data-bs-ride="carousel">
    <div class="carousel-indicators">
      <button v-for="(item,i) in slides" :key="i" type="button" data-bs-target="#carouselExampleCaptions" :data-bs-slide-to="i" class="active" aria-current="true" :aria-label="'Slide' +i+1"></button>
    </div>
    <div class="carousel-inner">
      <div v-for="(item,i) in slides" :key="i" class="carousel-item " :class="{active: i==0}" >
        <img :src="'http://localhost:8000'+item.image" class="d-block w-100" alt="...">
        <div class="carousel-caption d-none d-md-block">
          <h5>{{ item.title }}</h5>
          <p>{{ item.subTitle }}</p>
        </div>
      </div>
    </div>
    <button class="carousel-control-prev" type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide="prev">
      <span class="carousel-control-prev-icon" aria-hidden="true"></span>
      <span class="visually-hidden">Previous</span>
    </button>
    <button class="carousel-control-next" type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide="next">
      <span class="carousel-control-next-icon" aria-hidden="true"></span>
      <span class="visually-hidden">Next</span>
    </button>
  </div>


</template>

<script>
import {onBeforeMount, onMounted, ref} from "vue";

export default {
  name: "Slider",
  props:['slides'],
  setup() {




    return {

    }
  }

}
</script>


<style scoped>
p {
  text-align: center !important;
}
</style>