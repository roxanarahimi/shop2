<template>
  <div class="row">
    <div class="col-lg-3 mb-3">
      <div class="card h-100">
        <div class="card-body">
          <div class="bg-light rounded-circle mx-auto" style="width: 200px; height: 200px; overflow: hidden">
            <img src="/img/female.png" class="img-fluid mt-2" alt="">
          </div>
          <div class="d-flex justify-content-between ">
            <h6 class="mt-3 text-center fw-bold">{{ user.name }}</h6>
            <h6 class="mt-3 text-center fw-bold">{{ user.mobile }}</h6>
          </div>
        </div>
      </div>
    </div>
    <div class="col-lg-9 mb-3">
      <div class="card  h-100">
        <div class="card-body">
          <div class="text-start mb-3">
            <label class="labels fw-bold text-black-50">مشخصات</label>
            <hr class=" mb-4" style="margin-top: -2px;color: #dddddd">
          </div>
          <form>
            <div class="row">
              <div class="col-md-6 mb-2">
                <label class="label" for="name">نام</label>
                <input type="text" id="name" class="form-control form-control-sm" :value="user.name"/>
              </div>
              <div class="col-md-6 mb-2">
                <label class="label" for="gender">جنسیت</label>
                <select id="gender" class="form-select form-select-sm">
                  <option value=""></option>
                  <option value="female" :selected="user.gender == 'خانم' ? 'selectes' : false">خانم</option>
                  <option value="male" :selected="user.gender == 'آقا' ? 'selectes' : false">آقا</option>
                </select>
              </div>
              <div class="col-md-6 mb-2">
                <label class="label" for="mobile">موبایل</label>
                <input type="text" disabled id="mobile" class="form-control form-control-sm text-left " dir="ltr"
                       :value="user.mobile"/>
              </div>
              <div class="col-md-6 mb-2">
                <label class="label" for="email">ایمیل</label>
                <input type="email" id="email" class="form-control form-control-sm" :value="user.email"/>
              </div>

              <div class="col-12 mb-2">
                <input type="submit" class="btn btn-sm btn-dark float-start" @click.prevent="updateUser"
                       value="ویرایش"/>
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
  <div class="row">


    <div class="col-lg-12  mb-3">
      <div class="card h-100">
        <div class="card-body">
          <div class="text-start mb-3">
            <label class="labels fw-bold text-black-50">سفارش ها</label>
            <hr class=" mb-4" style="margin-top: -2px;color: #dddddd">
          </div>
          <div class="row">

            <div class="col-12 table-responsive">
              <table class="table text-start">
                <thead>
                <tr>
                  <th scope="col">کد سفارش</th>
                  <th scope="col">مبلغ</th>
                  <th scope="col" class="" style="width: 300px">وضعیت</th>
                  <th class="text-end" scope="col">تاریخ سفارش</th>
                  <th class="text-end" scope="col">جزییات</th>
                </tr>
                </thead>
                <tbody>
                <tr v-for="item in user.orders">
                  <th scope="row">{{ item.code }}</th>
                  <td>{{ item.amount }} T</td>
                  <td style="width: 300px" class="py-2">
                    <span>{{ item.status }}</span>
                    <div class="progress" style="height: 5px">
                      <div
                          :class="'progress-bar order_status rounded ' + item.color"
                          role="progressbar"
                          :style="'width: '+ item.percent+'%'"
                          :aria-valuenow="item.percent"
                          aria-valuemin="0"
                          aria-valuemax="100"></div>
                    </div>
                  </td>
                  <td class="text-end">{{ item.created_at }}</td>
                  <td class="text-end">
                    <router-link :to="'/order/'+item.id" class="btn btn-sm btn-dark">مشاهده</router-link>
                  </td>
                </tr>
                </tbody>

              </table>
            </div>
          </div>

        </div>
      </div>


    </div>
  </div>
  <div class="row">
    <div class="col-12 mb-3">
      <div class="card">
        <div class="card-body pb-0">
          <div class="text-start mb-3">
            <label class="labels fw-bold text-black-50">نشانی ها</label>
            <hr class=" mb-4" style="margin-top: -2px;color: #dddddd">
            <div>
              <div class="row">
                <div>
                  <table class="table">
                    <thead>
                    <tr>
                      <th scope="col">عنوان</th>
                      <th scope="col">استان</th>
                      <th scope="col">شهر</th>
                      <th scope="col">کد پستی</th>
                      <th scope="col">نشانی</th>
                      <th scope="col"></th>
                    </tr>
                    </thead>
                    <tbody>
                    <tr v-for="item in user.addresses">
                      <td>{{ item.title }}</td>
                      <td>{{ item.state.name }}</td>
                      <td>{{ item.city.name }}</td>
                      <td>{{ item.postal_code }}</td>
                      <td>{{ item.address }}</td>
                      <td>
                        <button class="btn btn-sm btn-dark" @click="showAddToEdit(item)" data-bs-toggle="modal"
                                data-bs-target="#EditModal">ویرایش
                        </button>
                      </td>
                    </tr>
                    </tbody>
                  </table>
                </div>
              </div>
            </div>
          </div>
          <div class="row">
          </div>
        </div>
      </div>

    </div>
    <div class="col-12 mb-3">
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

                  <select id="state" @change="findCities" class="form-select form-select-sm">
                    <option value=""></option>
                    <option v-for="item in states" :key="item.id" :value="item.id">{{ item.name }}</option>
                  </select>
                </div>
                <div class="col-3"><label for="city" class="form-label">شهر</label>
                  <select id="city" class="form-select form-select-sm">
                    <option v-for="item in state?.cities" :key="item.id" :value="item.id">{{ item.name }}</option>
                  </select>
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
                <div class="col-12 mb-2">
                  <input type="submit" class="btn btn-sm btn-dark float-start" @click.prevent="saveAdd" value="ثبت"/>
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


  <div class="modal fade" id="EditModal" data-bs-backdrop="static" data-bs-keyboard="false" tabindex="-1"
       aria-labelledby="staticBackdropLabel" aria-hidden="true">
    <div class="modal-dialog modal-dialog-centered modal-xl">
      <div class="modal-content">
        <div class="modal-body">
          <div class="card">
            <div class="card-body pb-0">
              <div class="text-start mb-3">
                <label class="labels fw-bold text-black-50">ویرایش نشانی</label>
                <hr class=" mb-4" style="margin-top: -2px;color: #dddddd">
                <div>
                  <input type="hidden" class="form-control form-control-sm" id="idEdit" required="">

                  <div class="row">
                    <div class="col-3">
                      <label for="title" class="form-label">عنوان</label>
                      <input type="text" class="form-control form-control-sm" id="titleEdit" required="">
                      <div class="form-text error"></div>
                    </div>
                    <div class="col-3">
                      <label for="state" class="form-label">استان</label>

                      <select id="stateEdit" @change="findCitiesE" class="form-select form-select-sm">
                        <option value=""></option>
                        <option v-for="item in states" :key="item.id" :value="item.id">{{ item.name }}</option>
                      </select>
                    </div>
                    <div class="col-3"><label for="city" class="form-label">شهر</label>
                      <select id="cityEdit" class="form-select form-select-sm">
                        <option v-for="item in citiesE" :selected="item.id === city_id" :key="item.id" :value="item.id">
                          {{ item.name }}
                        </option>
                      </select>
                    </div>
                    <div class="col-3">
                      <label for="postal_code" class="form-label">کد پستی</label>
                      <input type="text" class="form-control form-control-sm" id="postal_codeEdit" required="">
                      <div class="form-text error"></div>
                    </div>
                    <div class="my-2 col-12">
                      <label for="address" class="form-label">نشانی</label>
                      <textarea class="form-control form-control-sm" id="addressEdit" rows="2" required=""></textarea>
                      <div class="form-text error"></div>
                    </div>
                    <div class="col-12 mb-2">
                      <input type="submit" class="btn btn-sm btn-dark float-start" data-bs-dismiss="modal"
                             @click.prevent="updateAdd" value="ویرایش"/>
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
    </div>
  </div>
</template>

<script>
import {onMounted, ref} from "vue";
import Banner from "@/components/Banner";

export default {
  name: "Profile",
  components: {Banner},
  setup() {
    const user = ref('');
    const states = ref([]);
    const state = ref({});
    const citiesE = ref({});
    const city_id = ref({});
    onMounted(() => {
      getData();
    });
    const getData = () => {
      axios.get('http://localhost:8000/api/user/' + JSON.parse(localStorage.getItem('user')).id)
          .then((response) => {
            user.value = response.data;
            localStorage.setItem('user', JSON.stringify(response.data));
            console.log(response.data)
          });
      axios.get('http://localhost:8000/api/state')
          .then((response) => {
            states.value = response.data;
          })
    }
    const findCities = () => {
      axios.get('http://localhost:8000/api/state/' + document.getElementById('state').value)
          .then((response) => {
            state.value = response.data;
          })


    };
    const findCitiesE = () => {
      axios.get('http://localhost:8000/api/state/' + document.getElementById('stateEdit').value)
          .then((response) => {
            city_id.value = 0;
            citiesE.value = response.data.cities;
          })


    };
    const saveAdd = () => {
      axios.post('http://localhost:8000/api/address/user', {
        user_id: user.value.id,
        title: document.getElementById('title').value,
        city_id: document.getElementById('city').value,
        postal_code: document.getElementById('postal_code').value,
        address: document.getElementById('address').value,
      })
          .then((response) => {

            getData();
            document.getElementById('title').value = '';
            document.getElementById('state').value = '';
            document.getElementById('city').value = '';
            document.getElementById('postal_code').value = '';
            document.getElementById('address').value = '';
          })

    };
    const updateAdd = () => {
      axios.post('http://localhost:8000/api/address/user/' + document.getElementById('idEdit').value,
          {
            title: document.getElementById('titleEdit').value,
            city_id: document.getElementById('cityEdit').value,
            postal_code: document.getElementById('postal_codeEdit').value,
            address: document.getElementById('addressEdit').value,
          })
          .then((response) => {

            getData();
            document.getElementById('titleEdit').value = '';
            document.getElementById('stateEdit').value = '';
            document.getElementById('postal_codeEdit').value = '';
            document.getElementById('addressEdit').value = '';
            citiesE.value = '';
            city_id.value = 0;
          })

    };

    const updateUser = () => {
      axios.post('http://localhost:8000/api/user/' + JSON.parse(localStorage.getItem('user')).id, {
        name: document.getElementById('name').value,
        email: document.getElementById('email').value,
        gender: document.getElementById('gender').value,
      })
          .then((response) => {

            getData();
          });
    }

    const showAddToEdit = (address) => {
      citiesE.value = address.cities;

      city_id.value = address.city_id;

      document.getElementById('idEdit').value = address.id;
      document.getElementById('titleEdit').value = address.title;
      document.getElementById('stateEdit').value = address.city.state.id;
      document.getElementById('postal_codeEdit').value = address.postal_code;
      document.getElementById('addressEdit').value = address.address;
      document.getElementById('cityEdit').value = address.city_id;

    }
    return {
      user,
      getData,
      states,
      state,
      findCities,
      findCitiesE,
      saveAdd,
      updateAdd,
      updateUser,
      showAddToEdit,
      citiesE,
      city_id
    }
  }
}
</script>

<style scoped>
.label {
  margin-bottom: 5px;
  width: 100%;
  text-align: start;
}
</style>