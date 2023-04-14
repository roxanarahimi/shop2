<template>

  <div class="row  justify-content-center mb-3">
    <div class="col-12 col-md-8 col-lg-5  my-5">
      <div class="card">
        <div class="card-body">

          <div class="text-start ">
            <label class="labels fw-bold text-black-50">ورود به سایت</label>
            <hr class=" mb-4" style="margin-top: -2px;color: #dddddd">
          </div>

          <div id="mobileForm" class="row  pb-4 ">
            <p class="small mb-5 w-100 text-start">
            لطفا جهت ورود به سایت، شماره موبایل خود را وارد کنید
          </p>
            <div class="col-12 mb-3">
              <input type="text" id="mobile" placeholder="0912 - - - - - - -" class="text-end form-control form-control-sm"
                dir="ltr" minLength="11" maxLength="11">
            </div>
            <div class="col-12 d-flex ">
              <button  class="btn btn-sm btn-dark"  @click="getCode" >دریافت کد تایید</button>
            </div>
          </div>
          <div class="text-start mb-3 ">
            <li v-for="error in errors">{{ error }}</li>
          </div>
          <div id="codeForm" class="row  pb-4  d-none" dir="ltr">
            <p class="small mb-5 w-100 text-start">
              لطفا کد پیامک شده به تلفن همراه خود را وارد کنید
            </p>
            <div class="col-12 d-flex mb-3">
              <input type="text" id="code1" @input="autoTab($event)" minLength="1" maxLength="1" min="0" max="9"
                     class="text-center form-control form-control-sm mx-1">

              <input type="text" id="code2" @input="autoTab($event)" minLength="1" maxLength="1" min="0" max="9"
                     class="text-center form-control form-control-sm mx-1">

              <input type="text" id="code3" @input="autoTab($event)"  minLength="1" maxLength="1" min="0" max="9"
                     class="text-center form-control form-control-sm mx-1">

              <input type="text" id="code4" @input="autoTab($event)" minLength="1" maxLength="1" min="0" max="9"
                     class="text-center form-control form-control-sm mx-1">
            </div>
            <div class="col-12 d-flex justify-content-between px-3 ">
<!--              <button  class="btn btn-sm btn-dark"  @click="getCode" >دریافت کد تایید</button>-->
              <button @click="editNumber" class="btn btn-sm btn-dark">
                ویرایش شماره
              </button>
              <button disabled id="resend" @click="resend" class="btn btn-sm btn-dark">
                ارسال مجدد کد
                <span id="time">{{ time }}</span>
              </button>
            </div>



          </div>



          <div class="text-start">
            <li v-for="item in message"><small>{{ item }}</small></li>
          </div>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
import {onMounted, ref} from "vue";
import App from '../App';
export default {
  components:{App},
  setup() {
    onMounted(()=>{
      localStorage.clear();
    });
    const scope= ref('user');
    const errors= ref([]);
    const message= ref([]);
    const mobile = ref();
    const time = ref(59);
    onMounted(() => {
      document.getElementById("code1").value = '';
      document.getElementById("code2").value = '';
      document.getElementById("code3").value = '';
      document.getElementById("code4").value = '';
    });
    const getCode = () => {

      message.value = [];
      mobile.value = document.getElementById('mobile').value;
      if(mobile.value.length === 0){
        message.value.push('لطفا شماره موبایل را وارد کنید');
      }else{
        if (mobile.value.length  < 11){
          message.value.push('شماره موبایل باید 11 رقم باشد');
        }
        if(!mobile.value.startsWith('09')){
          message.value.push('شماره موبایل باید با 09 شروع شود');
        }
      }


      if(mobile.value.length === 11 && mobile.value.startsWith('09')){
        message.value = [];
        axios.post(App.data().apiUrl+'/api/otp/mobile', {
          mobile: document.getElementById('mobile').value,
          scope: 'user'
        }, {progress: false})
            .then((res) => {
              if (res.status === 200) {
                document.getElementById('mobileForm').classList.add('d-none');
                document.getElementById('codeForm').classList.remove('d-none');
              }else{
                // message.value = res;
                console.log(res)
              }
            })
            .then(()=>{
              document.getElementById('resend').setAttribute('disabled', 'disabled')
              counter();
              setTimeout(()=>{
                document.getElementById('resend').removeAttribute('disabled')
              },60000)
            })
            .catch((err) => {
              message.value = err.response.data.message;
            })
      }

    }

    const editNumber = ()=>{
      location.reload();
    }
    const resend = ()=>{

      getCode();
    }
    const counter=()=> {

      var distance = 59;
      var x = null;
      clearInterval(x);
      time.value = 0;
      x = setInterval(function () {

        // document.getElementById("time").classList.remove('d-none');


        distance--;
        time.value = distance;
        var t = time.value  < 10 ? "0" : "";
        document.getElementById("time").innerHTML = t + time.value ;

        if (distance < 1) {
          clearInterval(x);
          // document.getElementById("time").classList.add('d-none');

        }
      }, 1000);

      time.value = 0;
      // if(time.value === 0){
      //   document.getElementById('resend').removeAttribute('disabled')
      // }

    }
    const autoTab = (e) => {
      let code =
          document.getElementById("code1").value +
          document.getElementById("code2").value +
          document.getElementById("code3").value +
          document.getElementById("code4").value;

      if (code.length === 4) {

        axios.post(App.data().apiUrl+'/api/mobile/login', {
          mobile: document.getElementById('mobile').value,
          scope: 'user',
          password: document.getElementById("code1").value + document.getElementById("code2").value + document.getElementById("code3").value + document.getElementById("code4").value
        })
            .then((res) => {
              if (res.status === 200) {
                localStorage.setItem('user',JSON.stringify(res.data.user))
                localStorage.setItem('token',JSON.stringify(res.data.access_token))
                localStorage.setItem('scope',JSON.stringify(res.data.scope))
                localStorage.setItem('expire',JSON.stringify(res.data.expire));
                console.log(localStorage)
                window.location = '/';
              }else{
                console.log(res)
              }
            }).catch((err) => {
          message.value = err.response.data.message;
        })

      }

      if (e.target.value.length === e.target.maxLength) {
        e.target.nextElementSibling?.focus();
      }
    }

    return {
      autoTab, getCode, scope, message, mobile, counter, time, resend, editNumber, errors
    }
  }
}

</script>

<style scoped>

</style>