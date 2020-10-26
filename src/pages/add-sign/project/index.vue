<!--  -->
<template>
 <div class="enginUnit">
      <swiper class="swiper" :indicator-dots="indicatorDots" :duration="duration">
        <block>
            <swiper-item>
               <one-page />
            </swiper-item>
        </block>
        <block>
            <swiper-item>
              <two-page />
            </swiper-item>
        </block>
        <block>
            <swiper-item>
              <three-page />
            </swiper-item>
        </block>
        <block>
            <swiper-item>
              <four-page />
            </swiper-item>
        </block>
    </swiper> 
 </div>
</template>

<script>
import OnePage from "./swiperPage/onePage";
import TwoPage from "./swiperPage/twoPage";
import ThreePage from "./swiperPage/threePage";
import FourPage from "./swiperPage/fourPage";

export default {
  components:{
    OnePage,
    TwoPage,
    ThreePage,
    FourPage
  },
  data () {
    return {
      //是否显示画板指示点，根据图片数量自动生成多少个圆点
      indicatorDots: true,
      duration: 500,
      swiperCurrent: 0
    };
  },
}

</script>
<style lang='scss' scoped>
.enginUnit{
    height: 100%;
    .swiper{
        height: 100%;
    }
}
</style>