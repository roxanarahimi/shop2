<template>
  <div class="row mb-3">
    <div class="col-12">
      <div class="card">
        <div class="card-body">
          <div class="text-start mb-3">
            <label class="labels fw-bold text-black-50">سبد خرید</label>
            <hr class=" mb-4" style="margin-top: -2px;color: #dddddd">
          </div>
          <div class="row">

            <div class="col-12 table-responsive px-md-5">
              <table class="table text-start" v-if="cart.items != 0">
                <thead>
                <tr>
                  <th scope="col"></th>
                  <th scope="col"></th>
                  <th scope="col">عنوان</th>
                  <th scope="col">رنگ</th>
                  <th scope="col">سایز</th>
                  <th scope="col" class="text-center">تعداد</th>
                  <th scope="col">مبلغ</th>
                  <th scope="col">تخفیف</th>
                  <th scope="col"></th>
                </tr>
                </thead>
                <tbody>
                <tr v-for="(item, index) in cart.items" :key="index">
                  <th>{{ index+1 }}</th>
                  <td>
                    <img style="width: 80px; height: auto" :src="'http://localhost:8000'+item.product.images[0]" alt="">
                  </td>
                  <td>{{ item.product.title }}</td>
                  <td>{{ item.size.color_name }}</td>
                  <td>{{ item.size.size }}</td>

                  <td  class="text-center">
                    <button
                        class = "btn btn-dark btn-sm p-0 my-1  q-btn"
                        @click = "enscreaseQuantity(item.id, item.quantity)">+</button>
                    <input
                        :id = "'item_'+item.id"
                        class = "m-1 quantity fw-light text-center"
                        type = "number"
                        min = "1"
                        :value = "item.quantity"
                    />
                    <button
                        class = "btn btn-dark btn-sm p-0 my-1 q-btn"
                        @click = "decreaseQuantity(item.id, item.quantity)">-</button>
                  </td>
                  <td >{{ item.price }} T </td>
                  <td v-if="item.off" > {{ item.price * item.off / 100}}  T </td>
                  <td v-else ></td>
                  <td><button class="btn btn-dark btn-sm text-center p-0 bi bi-x q-btn" @click="removeItem(item.id)"></button> </td>
                </tr>
                </tbody>
              </table>
              <p v-else> سبد شما خالی است </p>
            </div>
          </div>
          <div class="d-flex justify-content-between">
            <router-link  v-if="cart.items != 0" to="/products" class="btn btn-sm btn-dark">ادامه خرید</router-link>
            <router-link  v-if="cart.items != 0" to="/confirm" class="btn btn-sm btn-dark">تایید سفارش</router-link>
          </div>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
import {onMounted, ref} from "vue";
import App from '../App.vue';
export default {
  name: "Cart",
  components: {App},
  setup(){
    const user = ref({});
    const cart = ref({});
    onMounted(()=>{
      getData();
    })
    const getData = () => {
      axios.get(App.data().apiUrl+'/api/user/' + JSON.parse(localStorage.getItem('user')).id)
          .then((response) => {
            user.value = response.data;
            localStorage.setItem('user', JSON.stringify(response.data));;
            response.data.allOrders.forEach((order)=>{
              if (order.status == 'سبد خرید'){
                cart.value = order;
              }
            })

            console.log('ccc',cart.value)
          })
          .catch();

    }

    const removeItem = (id) => {

      axios.post(App.data().apiUrl+'/api/remove/order/item/' + id,{
        order_item_id: id
      })
          .then((response)=>{

            getData();
          }).catch();
    };


    const enscreaseQuantity=(id)=> {
      let q = cart.value.items?.find((i) => i.id === id);
      q.quantity += 1;
      document.getElementById('item_' + id).value = q.quantity;


      updateQuantity(id, q.quantity);
      setTimeout(()=>{ getData();},300)

    }
    const decreaseQuantity = (id, quantity)=> {
      if (quantity > 1) {
        let z = cart.value.items?.find((j) => j.id === id);
        z.quantity -= 1;
        document.getElementById('item_' + id).value = z.quantity;

        updateQuantity(id, z.quantity);
        setTimeout(()=>{ getData();},300)

      }
    }
    const updateQuantity=(item_id, quantity)=> {
      axios.post(App.data().apiUrl+'/api/item/quantity/update', {item_id: item_id, quantity: quantity})
          .then((response) => {
            if (response.status === 200) {
              cart.value = response.data;
              if(document.getElementById('amount')) {
                document.getElementById('amount').innerText = this.cart.amount;
              }
            }

          })
          .catch((error) => {
            console.error(error);
            console.error(error.data)
            console.error(error.message)
            // console.log(error.data.message)

          });

    }


    return{
      getData, user, cart, removeItem,enscreaseQuantity, decreaseQuantity,updateQuantity
    }
  }

}
</script>

<style scoped>
tr{
}
td { vertical-align: bottom;
}
input[type="number"] {
  border-radius: 3px;
  border: 0px solid lightgray;
  background: white;
  height: 20px;
  width: 23px;
  font-size: 12px;
  text-align: center !important;
  margin-top: 2px;
  -moz-appearance: textfield;


}
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button
{
  -webkit-appearance: none;
  margin: 0;

}
.q-btn {
  width: 20px !important;
  height: 20px !important;
  line-height: 10px !important;
}
</style>