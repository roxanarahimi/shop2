<template>
  <div id="alert-success" class="alert alert-success d-flex align-items-center"
       style="width:500px; position: fixed; top:50px; right: calc(50% - 250px);
       z-index: 2000; transition: 0.5s ease; opacity: 0; " role="alert">
    <i style="font-size: 24px" class="bi bi-check-circle-fill me-2"></i>
    <div>
      این محصول به سبد خرید شما افزوده شد
    </div>
  </div>
  <div class="row justify-content-between">
    <div class="col-xl-8 mb-3">
      <div class="card h-100">
        <div class="card-body">

          <div class="row">
            <div class="col-9 mb-3  pe-0">
              <img id="img0" src="" class="img-fluid  " alt="">
            </div>
            <div class="col-3">
              <img id="img1" src="" class="img-fluid  mb-4" alt="">
              <img id="img2" src="" class="img-fluid mb-4" alt="">
              <img id="img3" src="" class="img-fluid " alt="">
            </div>

          </div>
        </div>
      </div>
    </div>
    <div class="col-md-6 col-xl-4 mb-3">
      <div class="card  h-100">
        <div class="card-body text-start">
          <div class=" mb-3">
            <label class="labels fw-bold text-black-50">موجودی</label>
            <hr class=" mb-4" style="margin-top: -2px;color: #dddddd">
          </div>
          <div class="row">
            <div class="col-md-12 mb-2">
              <label class="label">رنگ</label>
              <!--              <select id="color" class="form-select form-select-sm">-->
              <!--                <option v-for="item in colors" :value="item.color_name">{{ item.color_name }}</option>-->
              <!--              </select>-->

              <div id="colorsPart" class="d-flex w-100 py-1 ">
                <div v-for="(color,index) in colors" :key="index" class="color-border">
                  <div @click="selectColor(index)" class="color-circle" :data-name="color.color_name"
                       :style="'background-color:'+ color.color_code+';'"/>
                </div>
              </div>
              <p id="selected_color" class="mb-3 mt-1"></p>


            </div>

            <div class="col-md-12 mb-2">
              <label class="label" for="size_id">سایز</label>
              <select id="size_id" class="form-select form-select-sm m-0">
                <!--                            <option value = ""></option>-->
                <option @select="showDimensions(size.dimensions)" class="option " v-for="(size, i) in sizes" :key="i"
                        :value="size.id" :data-dimensions="size.dimensions">
                  {{ size.size }} {{ size.dimensions }}

                </option>
              </select>
              <div class="w-100 mt-3">
                <!--                <p id="dimensions"></p>-->
              </div>
            </div>
            <!--          </div>-->
            <!--          <div class="row">-->
            <div class="fw-bold mt-4 col-md-12 mb-2">
              <p>{{ product.title }}</p>
            </div>
            <div class="fw-bold col-md-12 mb-2 small">
              <p>{{ product.subtitle }}</p>
            </div>
            <div class="col-md-12 mb-0 ">
              <p class="d-inline me-3">{{ product.price - product.price * product.off / 100 }} تومان</p>
              <small v-if="product.off" class="text-decoration-line-through">{{ product.price }} </small>
            </div>
            <small class="flex-row-reverse d-flex justify-content-start mt-1 mb-3">
              <i class="bi me-1"
                 :class="{'bi-star-fill': product.score >= 1, 'bi-star' : product.score == 0,'text-warning': product.stock, 'bi-star-half ': 0 < product.score && product.score < 1 ,'text-muted': product.stock == 0}"></i>
              <i class="bi me-1"
                 :class="{'bi-star-fill': product.score >= 2, 'bi-star' : product.score < 2 && product.score < 1 ,'text-warning': product.stock, 'bi-star-half ': 1 < product.score && product.score < 2 ,'text-muted':product.stock == 0}"></i>
              <i class="bi me-1"
                 :class="{'bi-star-fill': product.score >= 3, 'bi-star' : product.score < 3 && product.score < 2,'text-warning': product.stock, 'bi-star-half ': 2 < product.score && product.score < 3 ,'text-muted': product.stock == 0}"></i>
              <i class="bi me-1"
                 :class="{'bi-star-fill': product.score >= 4, 'bi-star' : product.score < 4 && product.score < 3,'text-warning': product.stock, 'bi-star-half ': 3 < product.score && product.score < 4 ,'text-muted': product.stock == 0}"></i>
              <i class="bi me-1"
                 :class="{'bi-star-fill': product.score >= 5, 'bi-star' : product.score < 5 && product.score < 4,'text-warning': product.stock, 'bi-star-half ': 4 < product.score && product.score < 5 ,'text-muted': product.stock == 0}"></i>
            </small>


            <div>
              <button style="margin-top: 0" @click="addToCart" class="btn btn-sm btn-dark w-100">افزودن به سبد</button>

            </div>

          </div>
        </div>
      </div>
    </div>

    <div class="col-md-6 col-xl-4 mb-3">
      <div class="card h-100">
        <div class="card-body">
          <div class="text-start mb-3">
            <label class="labels fw-bold text-black-50">مشخصات</label>
            <hr class=" mb-4" style="margin-top: -2px;color: #dddddd">
          </div>
          <div class="row">

            <div class="col-12 table-responsive px-md-5">
              <table class="table text-start">
                <thead>
                </thead>
                <tbody>
                <tr v-for="item in features">
                  <th scope="row">{{ item.label }}</th>
                  <td style="text-align: justify">{{ item.value }}</td>
                </tr>


                </tbody>

              </table>
            </div>
          </div>

        </div>
      </div>


    </div>
    <div class="col-md-12 col-xl-8 mb-3">
      <div class="card h-100">
        <div class="card-body">
          <div class="text-start mb-3">
            <label class="labels fw-bold text-black-50">توضیحات</label>
            <hr class=" mb-4" style="margin-top: -2px;color: #dddddd">
          </div>
          <div class="row">

            <div class="col-12 table-responsive px-md-5">

              <p>
                {{ product.text }}
              </p>
            </div>
          </div>

        </div>
      </div>


    </div>
  </div>
</template>

<script>
import {onBeforeUnmount, onMounted, ref} from "vue";
import {useRoute} from "vue-router/dist/vue-router";
import App from '../App'

export default {
  name: "Product",
  components: {App},
  setup() {

    const user = ref(JSON.parse(localStorage.getItem('user')))
    const router = useRoute();
    const id = ref(router.params.id);
    const product = ref({});
    const colors = ref([]);
    const images = ref([]);
    const features = ref([]);
    const sizes = ref([]);

    const getData = () => {
      axios.get(App.data().apiUrl + '/api/product/' + id.value,)
          .then((response) => {
            product.value = response.data.product;
            features.value = JSON.parse(response.data.product.features);

            let q = response.data.colors;
            let i = 0;
            for (i; i <= 30; i++) {
              if (q[i]) {
                colors.value.push(JSON.parse(q[i]));
              }
            }
            console.log(response.data)
            console.log(colors.value)
            document.getElementById('img0').setAttribute('src', App.data().apiUrl + response.data.product.images[0])
            document.getElementById('img1').setAttribute('src', App.data().apiUrl + response.data.product.images[1])
            document.getElementById('img2').setAttribute('src', App.data().apiUrl + response.data.product.images[2])
            document.getElementById('img3').setAttribute('src', App.data().apiUrl + response.data.product.images[3])
          })
          .then(() => {
            showDimensions();
          })
          .then(() => {
            let b = document.querySelector('#colorsPart :nth-child(1)').firstChild.click();
          })
          .catch();


    };
    const addToCart = () => {




      if (user.value == null) {
        // alert(user.value)
        alert('لطفا برای سفارش محصول ابتدا از منوی ورود وارد اکانت خود شوید.')
      } else {


        axios.post(App.data().apiUrl + "/api/order", {
          user_id: JSON.parse(localStorage.user).id,
          product_id: product.value.id,
          product_size_id: document.getElementById('size_id').value,
          quantity: 1,
          price: product.value.price,
          off: product.value.off
        })
            .then((response) => {
              if (response.status === 200 || response.status === 201) {
                localStorage.setItem('expire', response.data.expire);
                localStorage.setItem('ppp', response.data.items.length);
                // if(localStorage.length){
                //
                //     document.getElementById('cart_count').innerHTML = response.data.items.length;
                // }

              }
            })
            .then(() => {
              // showToast.value = true;

              document.getElementById('alert-success').style.opacity = '0.95';
              document.getElementById('alert-success').style.top = '400px';
              setTimeout(() => {
                document.getElementById('alert-success').style.top = '-50px';
                document.getElementById('alert-success').style.opacity = '0';
              }, 3000);

              setTimeout(() => (this.showToast = false), 3000);


              // App.methods.updateUserInfo();
              // document.getElementById('cart_count').innerHTML = JSON.parse(localStorage.getItem('user')).cart?.items?.length || 0;

            })
            .catch((error) => {
              console.log(error);
            });
      }
    }
    onMounted(() => {

      getData();
    });

    const showDimensions = (txt) => {
      // alert(txt);
      // document.getElementById('dimensions').innerText = txt;
    }
    const selectColor = (index) => {
      if (document.querySelector('.selected_color')) {
        document.querySelector('.selected_color').classList.remove('selected_color');
      }
      if (document.querySelectorAll('.color-circle') && document.querySelectorAll('.color-circle')[index]) {
        document.querySelectorAll('.color-circle')[index].classList.add('selected_color');

      }
      if (document.querySelector('.selected_color')) {
        document.querySelector('#selected_color').innerText = document.querySelector('.selected_color').getAttribute('data-name');
      }
      if (document.querySelector('.selected_color')) {

        let color = document.querySelector('.selected_color').getAttribute('data-name');

        axios.get(App.data().apiUrl + "/api/sizes/product/" + id.value + '/' + color)
            .then(async (res) => {
              sizes.value = [];
              let j = 0;
              for (j; j < res.data.length; j++) {
                sizes.value.push((res.data)[j]);
              }
              document.querySelector('#dimensions').innerText = '';
            })
            .catch((err) => {
              console.log(err);
            });
      }
    };


    onBeforeUnmount(() => {
      document.getElementById('img0').setAttribute('src', '')
      document.getElementById('img1').setAttribute('src', '')
      document.getElementById('img2').setAttribute('src', '')
      document.getElementById('img3').setAttribute('src', '')

    })
    return {
      id, product, colors, images, addToCart, getData, router, features, showDimensions, selectColor, sizes, user
    }
  },

}
</script>

<style scoped>
.color-border {
  border: 3px solid cadetblue;
  border-radius: 50%;
  margin: 1px;
  cursor: pointer;
  background-color: lightgray !important;

}

.color-circle {
  width: 18px;
  height: 18px;
  border-radius: 50%;
  margin: 2px;
}

.selected_color {
  width: 22px !important;
  height: 22px !important;
  margin: 0 !important;

}

</style>