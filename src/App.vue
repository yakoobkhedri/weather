<template>
  <div class="card mx-auto mt-5 text-center" style="width: 22rem;">
  <img src="./assets/weather.png" class="card-img-top" alt="...">
  <div class="card-body">
    <div class="input-group mb-3">
      <button class="btn btn-primary" type="button" id="button-addon1" @click="getData">ارسال</button>
      <input type="text" class="form-control text-end" v-model="city" placeholder="اسم شهر را وارد کنید" aria-label="Example text with button addon" aria-describedby="button-addon1">
  </div>
  <div class="card-text" v-if="data" style="direction: rtl;">
          <p>اسم شهر: {{ data.name }}</p>
          <p>دما: {{ data.main.temp }}</p>
          <p>توضیحات: {{ data.weather[0].description }}</p>
          <p>سرعت باد: {{ data.wind.speed }}</p>
        </div>
        <p class="card-text" v-else-if="isLoading">
          در حال دریافت اطلاعات...
        </p>
  </div>
</div>
</template>

<script>
import axios from 'axios'
const API_KEY='ad7e9cc7a52ef561b1c604c0c72d92e3';
export default{
  name:'app',
  data() {
    return {
      city:'',
      data: null,
    isLoading: false
    }
  },
   methods:{
    getData(){
      this.isLoading = true;
       axios.get(`https://api.openweathermap.org/data/2.5/weather`, {
        params: {
          q: this.city,
          appid: API_KEY,
          units: 'metric',
          lang: 'fa'
        }
      }).then(({data})=>{
        this.isLoading = false;
          this.data=data;
      })
    }
  }
}
</script>
