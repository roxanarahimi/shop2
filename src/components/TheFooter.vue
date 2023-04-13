<template>
  <footer class="row m-0 justify-content-center rounded-top bg-2">
    <div class="row col-xl-10 mt-5" >
      <div class="col-6 col-md-2 mt-4" >

        <img src="img/enamad.png" class="img-fluid" alt="">
      </div>
      <div class="col-6 col-md-2 mt-4" >
        <p class="h6 fw-bold mb-3" >حساب کاربری</p>
        <p >
          <a href="/" class="router-link-active router-link-exact-active d-block "
             aria-current="page">پروفایل من</a>
        </p>
        <p >
          <a href="/" class="router-link-active router-link-exact-active d-block "
             aria-current="page">سفارش ها</a>
        </p>
        <p >
          <a href="/" class="router-link-active router-link-exact-active d-block "
             aria-current="page">خروج</a>
        </p>
      </div>
      <div class="col-12 col-md-8 mt-4 mb-3" >
        <p class="h6 fw-bold mb-3" >تماس با ما</p>
        <p class="" >نشانی: تهران شیان خیابان شهید فرشادی نبش کوچه خندان پلاک ۵ ساختمان آراتل طبقه
          دوم</p>
        <p class="" >ایمیل: webagent.ir@gmail.com</p>
        <p class="" >تلفن: <a class="" href="tel:09032313681" dir="ltr" >0903
          231 36 81</a></p>
        <div class="social-links mt-3 d-flex justify-content-end" >
          <a class="mx-2 a" style="{font-size:13px}" href="tel:09032313681" >
            <i class="bi bi-telephone-fill" ></i>
          </a>
          <a class="mx-2 a" target="_blank" href="https://linkedin.com/in/roxanarahimi" >
            <i class="bi bi-linkedin" ></i>
          </a>
          <a class="mx-2 a" target="_blank" href="https://api.whatsapp.com/send?phone=989032313681" >
            <i class="bi bi-whatsapp" ></i>
          </a>
          <a class="mx-2 a" target="_blank" href="https://t.me/webagent_ir" >
            <i class="bi bi-telegram" ></i>
          </a>
          <a class="mx-2 a" target="_blank" href="https://www.instagram.com/webagent.ir" >
            <i class="bi bi-instagram" ></i></a>
        </div>
      </div>
      <hr >
      <small class="mb-2" > © رکسانا رحیمی 1401 </small>
    </div>
  </footer>

</template>

<script>
export default {
  name: "TheFooter"
}
</script>

<style scoped>
*, a{
  color: white;
}
/**:not(.bi), a:not(.a){*/
/*  color: white;*/
/*}*/
/*.a {*/
/*  !*color: #42b983;*!*/
/*  color: #ff667d !important;*/
/*  text-shadow: 1px 1px #eeeeee;*/
/*}*/


</style>