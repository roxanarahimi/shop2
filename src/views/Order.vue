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
                <tr v-for="item in 3">
                  <td style="width: 120px">
                    <img style="width: 120px; height: auto" src="http://localhost:8080/img/blog8-1355x1020.jpg" alt="">
                  </td>
                  <td style="direction: rtl">
                    <div>
                      <p class="fw-bold">کراپ تاپ</p>
                      <small>تک سایز</small> -
                      <small>مشکی</small>
                    </div>
                  </td>
                  <td style="width: 50px">2</td>
                  <td>500000T</td>
                  <td>-50000T</td>
                  <td>900000T</td>
                </tr>
                <tr class="border-top">

                  <td class="fw-bold pt-5" colspan="2">
                    <i class="bi bi-heart-fill" style="color: hotpink"></i>
                    با تشکر از خرید شما
                  </td>
                  <td class="fw-bold pt-5" colspan="4">
                    <p>                    تخفیف  : 1.500.000
                    </p>
                    <p class=" ">                    هزینه ارسال  : 1.500.000
                    </p>
                    <p class=" mb-0">پرداخت شما  : 2.700.000
                    </p>

                  </td>
                </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="col-xl-4 mb-3">
      <div class="card">
        <div class="card-body text-start">
          <div class="card-body" ><p class="fw-bold mb-1" >نشانی:</p><small
              class="text-muted" >تهران تهران شیان خیابان شهید فرشادی نبش کوچه خندان پلاک ۵ ساختمان آراتل طبقه دوم</small>
            <p class="fw-bold mb-1" >کد پستی:</p><small class="text-muted" >1736521458</small>
            <p class="fw-bold mb-1 mt-3" >وضعیت:</p><small class="text-muted" >در حال آماده سازی</small>
            <button class="btn btn-sm btn-secondary mx-3" style="float: left"  data-bs-toggle="modal" data-bs-target="#confirmModal">لغو سفارش</button>
            <p class="fw-bold mb-1 mt-3" >کد رهگیری پست:</p><small class="text-muted" >
              <span class="mx-2" ><svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" fill="currentColor" class="bi bi-clipboard" viewBox="0 0 16 16"><path d="M4 1.5H3a2 2 0 0 0-2 2V14a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V3.5a2 2 0 0 0-2-2h-1v1h1a1 1 0 0 1 1 1V14a1 1 0 0 1-1 1H3a1 1 0 0 1-1-1V3.5a1 1 0 0 1 1-1h1v-1z"></path><path d="M9.5 1a.5.5 0 0 1 .5.5v1a.5.5 0 0 1-.5.5h-3a.5.5 0 0 1-.5-.5v-1a.5.5 0 0 1 .5-.5h3zm-3-1A1.5 1.5 0 0 0 5 1.5v1A1.5 1.5 0 0 0 6.5 4h3A1.5 1.5 0 0 0 11 2.5v-1A1.5 1.5 0 0 0 9.5 0h-3z"></path></svg></span></small><small class="d-block text-muted mb-1 mt-3"> برای پیگیری وضعیت بسته کد رهگیری
              را کپی و در <a class="fw-bold" href="https://tracking.post.ir/" target="_blank" >اینجا</a>
              جستوجو کنید </small></div>
        </div>
      </div>
    </div>

  </div>

  <div class="modal fade" id="confirmModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header border-0">
        </div>
        <div class="modal-body">
          آیا سفارش لغو شود؟
        </div>
        <div class="modal-footer border-0">
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">نه!</button>
          <button type="button" class="btn btn-primary" data-bs-dismiss="modal">بله</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Order"
}
</script>

<style scoped>
td{
  border: none;
  vertical-align: bottom;
  direction: ltr;
}
</style>