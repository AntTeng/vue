<template>
  <div>
    <header class="header">
        <div class="back iconfont">&#xe624;</div>
        <div class="search"></div>
        <div class="city">城市</div>
    </header>
    <swiper :options="swiperOption">
    <!-- slides -->
    <swiper-slide v-for="item in swiperInfo" :key="item.id">
      <div class="swiper-img-icon">
        <img class="swiper-img" :src="item.imgUrl"/>
      </div>
    </swiper-slide>
    <!-- Optional controls -->
    <div class="swiper-pagination"  slot="pagination"></div>
    </swiper>
    <div>123123132</div>
  </div>
</template>

<script>
export default {
  name: 'Index',
  data () {
    return {
      swiperInfo: [],
      iconInfo: [],
      swiperOption: {
        autoplay: 10000,
        direction: 'horizontal',
        pagination: '.swiper-pagination',
        loop: true
      }
    }
  },
  created () {
    this.getIndexData()
  },
  methods: {

    getIndexData () {
      this.$http.get('static/index.json')
        .then(this.handleGetDataSucc.bind(this))
    },

    handleGetDataSucc (res) {
      const body = res.body
      if (body && body.data && body.data.swiper) {
        this.swiperInfo = body.data.swiper
        this.iconInfo = body.data.icons
        console.log(res)
      }
    }
  }
}
</script>

<style scoped>
    .header {
        display: flex;
        height: 0.86rem;
        background: #05bad5;
        color: #fff;
    }
    .back {
        width: .64rem;
        line-height: .86rem;
        text-align: center;
    }
    .search{
        flex: 1;
        margin: .14rem .18rem;
        background: #fff;
        border-radius: .1rem;
    }
    .city {
        width: 1.14rem;
        line-height: .86rem;
        text-align: center;
    }
    .swiper-img-con{
      width: 100%;
      /*height: 31.25vh;*/
      height: 0;
      padding-bottom: 31.25%;
    }
    .swiper-img{
      width: 100%;
    }
</style>
