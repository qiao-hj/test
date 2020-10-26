<!-- 我的签到 -->
<template>
<div class="swiperDiv">
  <div class="mySignBox" v-if="isSign">
     <swiper class="swiper" indicatorDots>
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
         <block>
            <swiper-item>
              <five-page />
            </swiper-item>
        </block>
    </swiper> 
  </div>
  <div v-else style="height:100%">
     <scroll-view scroll-x style="height: 40px;" class="top">
       <div class="tabbar" :class="{'tabbar-bottom':currentTab==index}" v-for="(item,index) in tabBar" :key="index" @click="clickTab(index)">
              {{item.title}}
        </div>
      </scroll-view>
      <swiper :current="currentTab" @change="changeTab" style="height: 100%">
        <swiper-item>
          <ul class="pendding">
            <li @click="signHandle">
              <img src="/static/images/ticket.jpg" alt="">
              <div class="textRight">
                <div class="iconleft">
                  <p>扫码签到</p>
                  <span>发起人: 快乐星球特..</span>
                </div>
                <div class="iconRight">
                  <img src="/static/images/five.png" alt="收藏" class="fivePng">
                  <img src="/static/images/dot.png" alt="更多" class="more">
                </div>
                <span v-if="signed" class="signed">已签到</span>
              </div>
            </li>
           <li @click="signHandle">
              <img src="/static/images/ticket.jpg" alt="">
              <div class="textRight">
                <div class="iconleft">
                  <p>扫码签到</p>
                  <span>发起人: 快乐星球特..</span>
                </div>
                <div class="iconRight">
                  <img src="/static/images/five.png" alt="收藏" class="fivePng">
                  <img src="/static/images/dot.png" alt="更多" class="more">
                </div>
                <span  class="signed" v-if="!signed">已签到</span>
              </div>
            </li>
          </ul>
        </swiper-item>
        <swiper-item>
           未开始
        </swiper-item>
        <swiper-item>
          已结束
        </swiper-item>
      </swiper>
  </div>
</div>
</template>

<script>
import OnePage from "./swiperTable/onePage";
import TwoPage from "./swiperTable/twoPage";
import ThreePage from "./swiperTable/threePage";
import FourPage from "./swiperTable/fourPage";
import FivePage from "./swiperTable/fivePage";

export default { 
  components: {
    OnePage,
    TwoPage,
    ThreePage,
    FourPage,
    FivePage
  },
  data () {
    return {
      //是否显示画板指示点，根据图片数量自动生成多少个圆点
      indicatorDots: true,
      swiperCurrent: 0,
      isSign: false,
      signed: false,
      tabBar: [{
        id: 0,
        title: "进行中"
      },{
        id: 1,
        title: "未开始"
      },{
        id: 2,
        title: "已结束"
      }],
      currentTab: 0
    };
  },
  methods:{
    clickTab(e){
     this.currentTab = e;
    },
    signHandle(){
      if(this.signed){
        // 未签到
        this.isSign = true;
      }else{
        wx.navigateTo({
          url: "./scan/main"
        });
      }
    }
  },
  onLoad(){
    // this.isSign = getApp().globalData.isSign;
  }
}

</script>
<style lang="scss" scoped>
.mySignBox,.swiperDiv{
  height: 100%;
  background: rgba(243, 240, 240, 0.973);
  .swiper{
    padding-top: 10px;
    height: 100%;
    background: #fff;
  }
}
.pendding{
  height: 100%;
  background: #eee;
  li{
    display: flex;
    background: #fff;
    justify-content: space-around;
    align-items: center;
    padding: 0 10px;
    box-sizing: border-box;
    height: 100px;
    border-top: 5px solid #eee;
    &:first-child{
      border-top: 1.5px solid #eee;
    }
    >img{
      width: 80px;
      height: 60px;
      border-radius: 5px;
      position: relative;
      &:before{
        content: "";
        display: inline-block;
        position: absolute;
        left: 0;
        top:0;
        width:100%;
        height:100%;
        background: rgba(0, 0, 0, 0.4);
      }
    }
    .textRight{
      width:70%;
      position: relative;
      .iconleft{
        font-size: 16px;
        p{
         line-height: 35px;
        }
        span{
          font-size: 12px;
          line-height: 30px;
          color: #999;
        }
      }
      .iconRight{
        position: absolute;
        top:0;
        right: 0;
        .more{
          width: 12px;
          height: 15px;
        }
        .fivePng{
          width: 18px;
          height: 18px;
          margin-right: 18px;
          color: #999;
        }
      }
      .signed{
        position: absolute;
        bottom: 0px;
        right: 10px;
        color: #fff;
        font-size: 12px;
        padding: 5px 18px;
        background: rgb(143, 140, 140);
        border-radius: 50px;
      }
    }
  }
}
.top {
  width: 100%;
  text-align: center;
  background: #fff;
  line-height: 42px;
  white-space: nowrap;
  position: relative;
}
.tabbar {
  width: 120px;
  font-size: 14px;
  height: 42px;
  display: inline-block;
  color: #999;
  font-weight: 600;
 }
 
 .tabbar-bottom {
  color: #199ED8;
  border-bottom: 3px solid #199ED8;
 }
</style>