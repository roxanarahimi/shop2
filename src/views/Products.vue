<template>
  <div class="row">
    <div class="col-5 col-md-3 h-100 products_side">
      <div class="card ps-3 ps-xl-5 pe-3 pt-5 pb-5 ">
        <div class="form-check mx-1">
          <input class="form-check-input" @change="getInfo" type="checkbox" id="stock"/>
          <label class="form-check-label" for="stock">کالاهای موجود</label>
        </div>
        <div class="form-check mx-1">
          <input class="form-check-input" type="checkbox" @change="getInfo" value="" id="off">
          <label class="form-check-label" for="off">
            تخفیف
          </label>
        </div>
<!--        <hr class="text-muted">-->
        <p class="fw-bold mt-3">دسته بندی</p>
        <div v-for="item in categories" class="form-check mx-1">
          <input class="form-check-input" type="checkbox" @change="getInfo" name="cat_id" :value="item.id"
                 :id="'cat_'+item.id">
          <label class="form-check-label" :for="'cat_'+item.id">
            {{ item.title }}
          </label>
        </div>


      </div>
    </div>

    <div class="col-7 col-md-9" style="min-height: 500px !important">
      <div class="row p-0 m-0">
        <div class="col-12 p-0 m-0 mb-3">
          <div class="card">
            <div class="card-body">
              <nav id="sortNav" class=" text-start py-0 px-2 small">
                <a class="sort pointer active-sort" id="new" @click="sortBy('new')">جدید ترین </a>
                <a class="sort pointer" id="sale" @click="sortBy('sale')">پرفروش ترین </a>
                <a class="sort pointer" id="view" @click="sortBy('view')">پر بازدید ترین </a>
                <a class="sort pointer" id="score" @click="sortBy('score')">محبوب ترین </a>
                <a class="sort pointer" id="cheap" @click="sortBy('cheap')">ارزان ترین </a>
                <a class="sort pointer" id="expensive" @click="sortBy('expensive')">گران ترین </a>
              </nav>
            </div>
          </div>
        </div>
        <div class="col-12 p-0 m-0" v-if="products.length">
          <div class="mx-auto row  pb-5 pt-2 ">
            <div v-for="product in products" :key="product.id" class=" col-12 col-md-6 col-lg-4 col-xl-3 col-xxl-3 p-1">
              <div class=" border border rounded ">
                <productCard :product="product"/>
              </div>
            </div>
          </div>
        </div>
        <div class="col-12" v-else>
          <!--                        <p id = "msg" class = "my-4">درحال بار گذاری... </p>-->
          <p id="msg" class="my-4"></p>
        </div>
        <div class="col-12" id="loader">
          <loader/>
        </div>
      </div>


    </div>
  </div>
</template>

<script>
import ProductCard from "@/components/ProductCard";
import App from "@/App"

export default {
  name: "Products",
  components: {ProductCard},
  data() {
    return {
      products: [],
      categories: [],
    }
  },
  mounted() {
    document.getElementById('search').addEventListener('input',this.getInfo)
    document.addEventListener('scroll', () => {
      let top = document.documentElement.scrollTop;
      if (document.querySelector('.products_side > .card') && top > 100) {
        document.querySelector('.products_side > .card')?.setAttribute('style', 'top:10px');
      } else {
        document.querySelector('.products_side > .card')?.removeAttribute('style');
      }
    });
    //this.load();
    this.getCategories();
    this.getInfo();
  },
  methods: {
    getInfo() {
      let cats = '';
      document.getElementsByName('cat_id').forEach((c) => {
        if (c.checked === true) {
          if (cats !== '') {
            cats += ',';
          }
          cats += c.value;
        }
      })

      this.products = [];
      let params = '?stock=' + document.getElementById('stock').checked + '&cat_ids=' + cats
          + '&off=' + document.getElementById('off').checked
          + '&sort=' + document.querySelector('.active-sort').getAttribute('id')
          + '&search=' + document.getElementById('search').value + '&limit=&sale=false'
      ;

      console.log(params)
      document.getElementById('loader').classList.remove('d-none');
      fetch(App.data().apiUrl + "/api/product" + params)
          .then((res) => res.json())
          .then(async (data) => {

            await setTimeout(() => {
              document.getElementById('loader')?.classList.add('d-none');
            }, 500);
            await setTimeout(() => {
              this.products = data;
              if (document.getElementById('msg')) {
                if (this.products.length === 0) {
                  document.getElementById('msg').innerText = 'محصولی پیدا نشد';
                } else {
                  document.getElementById('msg').innerText = 'درحال بار گذاری...';
                }
              }

            }, 600);

          })
          .catch((err) => console.log(err.message));

    },
    getCategories() {
      fetch(App.data().apiUrl + "/api/category/product")
          .then((res) => res.json())
          .then((data) => {

            this.categories = data;

          })
          .catch((err) => console.log(err.message));
    },
    async sortBy(property) {
      function a() {
        let prev = document.querySelector(".active-sort");
        prev.classList.remove("active-sort");

        var element = document.getElementById(property);
        element.classList.add("active-sort");
      }

      await a();
      await this.getInfo();


    }
  }
}
</script>

<style>
.card {
  border: 0px !important;
}

label, input[type=checkbox] {
  cursor: pointer;
}



.product-card {
  border: 0px !important;
}

@media (min-width: 1200px) {
  .products_side .card {
    /*border: 1px solid lightgray;*/
    /*border-right: none;*/
    /*border-radius: 3px;*/
    /*position: -webkit-sticky !important; !* Safari *!*/
    /*position: sticky !important;*/
    /*top: 0 !important;*/

    transition: 1s ease;
    position: fixed;
    width: 250px;
    text-align: start !important;
  }
}

</style>