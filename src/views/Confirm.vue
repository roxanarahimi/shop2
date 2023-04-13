<template>
  <div class="row">
    <div class="col-xl-8 mb-3">
      <div class="card">
        <div class="card-body">
          <div class="text-start mb-3">
            <label class="labels fw-bold text-black-50">فاکتور خرید</label>
            <hr class=" mb-4" style="margin-top: -2px;color: #dddddd">
          </div>
          <div class="row">

            <div class="col-12 table-responsive px-md-5">
              <table class="table text-start">
                <tbody>
                <tr v-for="item in cart.items">
                  <td style="width: 120px">
                    <img style="width: 120px; height: auto" :src="'http://localhost:8000'+ item.product.images[0]" alt="">
                  </td>
                  <td style="direction: rtl">
                    <div>
                      <p class="fw-bold">{{ item.product.title }}</p>
                      <small>{{ item.size.size }}</small> -
                      <small>{{ item.size.color_name }}</small>
                    </div>
                  </td>
                  <td style="width: 50px">{{ item.quantity }}</td>
                  <td>{{ item.price }}T</td>
                  <td v-if="item.off">{{ item.price * item.off / 100 * -1 }}T</td>
                  <td v-else></td>
                  <td>{{ item.quantity * item.price * (1 - (item.off / 100)  ) }} T</td>
                </tr>
                <tr class="border-top">

                  <td class="fw-bold pt-5" colspan="2">
                    <i class="bi bi-heart-fill" style="color: hotpink"></i>
                    با تشکر از خرید شما
                  </td>
                  <td class="fw-bold pt-5" colspan="4">
                    <p> تخفیف  : {{ off }}</p>
                    <p class=""> هزینه ارسال  : 15000 </p>
                    <p class=" mb-0"> پرداخت شما  : {{ cart.amount}} </p>

                  </td>
                </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="col-xl-4 mb-3 ">
      <div class="card ">
        <div class="card-body">
          <div class="text-start mb-3">
            <label class="labels fw-bold text-black-50">نشانی پستی</label>
            <hr class=" mb-4" style="margin-top: -2px;color: #dddddd">
          </div>
          <div class="row">
            <div class="row">
              <div class="col-8 mb-3 text-start">
<!--                <label for="title" class="form-label">عنوان</label>-->
                <select class="form-select form-select-sm" id="address1" required="" @change="showAdd">
                  <option v-for="item in user.addresses" :selected="item.id == cart.address_id" :value="item.id">{{  item.title }}</option>
                </select>

                <div class="form-text error"></div>
              </div>
              <p id="stateAdd"></p>
              <p id="cityAdd"></p>
              <p id="codeAdd"></p>
              <p id="addAdd"></p>


<!--              <div class="text-end">-->
<!--                <button class="btn btn-sm btn-dark" data-bs-toggle="modal" data-bs-target="#staticBackdrop">نشانی جدید</button>-->
<!--              </div>-->
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="col-12">
      <button class="bn btn-lg btn-dark mb-3" @click="payOrder(cart.id)">تایید و پرداخت</button>
    </div>
  </div>


  <!-- Modal -->
  <div class="modal fade" id="staticBackdrop" data-bs-backdrop="static" data-bs-keyboard="false" tabindex="-1" aria-labelledby="staticBackdropLabel" aria-hidden="true">
    <div class="modal-dialog modal-dialog-centered modal-xl">
      <div class="modal-content">
<!--        <div class="modal-header">-->
<!--          <h5 class="modal-title" id="staticBackdropLabel">Modal title</h5>-->
<!--          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>-->
<!--        </div>-->
        <div class="modal-body pb-0">
          <div class=" mb-3">
            <div class="card">
              <div class="card-body pb-0">
                <div class="text-start mb-3">
                  <label class="labels fw-bold text-black-50">ثبت نشانی جدید</label>
                  <hr class=" mb-4" style="margin-top: -2px;color: #dddddd">
                  <div>
                    <div class="row">
                      <div class="col-3">
                        <label for="title" class="form-label">عنوان</label>
                        <input type="text" class="form-control form-control-sm" id="title" required="">
                        <div class="form-text error"></div>
                      </div>
                      <div class="col-3">
                        <label for="state" class="form-label">استان</label>
                        <input type="text" class="form-control form-control-sm" id="state" required="">
                        <div class="form-text error"></div>
                      </div>
                      <div class="col-3"><label for="city" class="form-label">شهر</label>
                        <input type="text" class="form-control form-control-sm" id="city" required="">
                        <div class="form-text error"></div>
                      </div>
                      <div class="col-3">
                        <label for="postal_code" class="form-label">کد پستی</label>
                        <input type="text" class="form-control form-control-sm" id="postal_code" required="">
                        <div class="form-text error"></div>
                      </div>
                      <div class="my-2 col-12">
                        <label for="address" class="form-label">نشانی</label>
                        <textarea class="form-control form-control-sm" id="address" rows="2" required=""></textarea>
                        <div class="form-text error"></div>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="row">
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="modal-footer border-0">
          <button class="btn btn-sm btn-dark" data-bs-dismiss="modal">ثبت نشانی</button>
          <button class="btn btn-sm btn-secondary" data-bs-dismiss="modal">انصراف</button>


        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {onMounted, ref} from "vue";

export default {
  name: "Confirm",
  setup(){
    const user = ref({});
    const cart = ref({});
    const off = ref(0);
    const address = ref({});
    onMounted(()=>{
      getData();

    })
    const getData = () => {
      axios.get('http://localhost:8000/api/user/' + JSON.parse(localStorage.getItem('user')).id)
          .then((response) => {
            user.value = response.data;
            localStorage.setItem('user', JSON.stringify(response.data));
            console.log(response.data)
            console.log(response.data.allOrders);
            response.data.allOrders.forEach((order)=>{
              if (order.status == 'سبد خرید'){
                cart.value = order;
              }
            })

          })
      .then(()=>{
        showAdd();

        let totalOff = 0;
        cart.value.items.forEach((item)=>{
          let off = item.quantity * item.price * item.off/100;
          totalOff += off;
        })

        off.value = totalOff;
        console.log( off.value, amount.value)
      }).catch();

    }
    const showAdd = () => {
      axios.get('http://localhost:8000/api/address/user/' + document.getElementById('address1').value)
          .then((response)=>{
            console.log(response.data)
            let add = response.data;
            document.getElementById('stateAdd').innerText= add.city.state.name;
            document.getElementById('cityAdd').innerText= add.city.name;
            document.getElementById('codeAdd').innerText= 'کد پستی ' + add.postal_code;
            document.getElementById('addAdd').innerText= add.address;

          }).then(()=>{
        updateOrderAdd();
      }).catch();



          console.log('add',document.getElementById('address1').value)
    };
    const updateOrderAdd = () => {
      axios.post('http://localhost:8000/api/order/' + cart.value.id,{
        user_address_id: document.getElementById('address1').value
      })
          .then((response)=>{
            console.log(response.data)
          }).catch();
 };

    const payOrder = (id)=>{
      axios.post('http://localhost:8000/api/pay/order/'+ id)
      .then((response)=>{
        console.log(response.data)
        window.location = response.data.url;
      })
      ;
    }
    return{
      getData, user, cart, address, showAdd, updateOrderAdd,off, payOrder
    }
  }
}
</script>

<style scoped>
td{
  border: none;
  vertical-align: bottom;
  direction: ltr;
}
</style>