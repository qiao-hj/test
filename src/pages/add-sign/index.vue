<template>
  <div class="createSign">
    <div class="projectList">
        <img src="/static/images/ticket.jpg" alt="">
        <button @click="writeProject">点击填写工程单 (必填)</button>
        <div class="mask"></div>
    </div>
    <div class="signRules">
      <h6>签到规则</h6>
      <p>微信「扫一扫」扫描二维码即可参与签到</p>
      <p>参与签到需填写个人姓名</p>
      <ul class="ruleInfo">
        <li @click="changeStartTime">
          开始日期
          <span >{{startDate}} <i class="iconfont icon-left"></i></span>
        </li>
        <li @click="changeEndTime">
          结束日期
          <span>{{endDate}} <i class="iconfont icon-left"></i></span>
        </li>
        <li>
          签到周期
          <span>每天</span>
        </li>
        <li :class="{'signTimeLi': isShow}" :style="{height: tHeight}" id="signTimeLi">
          <div class="signTimeLeft">
            每天可签到时间
            <span class="signTime">
              <i v-for="(i,n) in days" :key="n" @click="selectType(n)" :class="cur == n?'active': ''">{{i}}</i>
            </span>
          </div>
          <div class="timeSlot" v-if="isShow">
            <div class="allTimeSlot">
              <div class="timeDiv" v-for="count in addTimeCount" :key="count">
                <small class="delicon" @click="delTimeSlot">x</small>
                <p>时段1开始时间 <span @click="selectStart">
                  <!-- 时间组件 -->
                  <picker mode="time" :value="startTime" start="09:01" end="21:01" @change="timeChange($event)" v-if="isShowTime" style="display: -webkit-inline-box">
                    <view class="picker">
                      {{startTime}}
                    </view>
                  </picker>
                  <i class="iconfont icon-left"></i></span> </p>
                <p>时段1结束时间 <span @click="selectEnd">
                   <picker mode="time" :value="endTime" start="09:01" end="21:01" @change="timeChange($event)" v-if="isShowTime" style="display: -webkit-inline-box">
                    <view class="picker">
                      {{endTime}}
                    </view>
                  </picker>
                  <i class="iconfont icon-left"></i></span> </p>
              </div>
            </div>
            <p @click="addTimeSlot"><em>+</em> 继续添加可签到时段</p>
          </div>
        </li>
        <li>
          每天可签到次数
          <number-box @numberBoxChange="retrunResult" />
          <!-- <span>1 <i class="iconfont icon-left"></i></span> -->
        </li>
        <li :class="{'signSite': isChecked}" :style="{height: sHeight}">
          <div class="signSiteLeft">
             必须在指定地点才能签到
            <span>
              <switch :checked="isChecked" @change="changeSignFlag" style="zoom: 0.5" color="#1a79c8"  />
            </span>
          </div>
          <div class="showSite"  v-if="isChecked">
            <div class="siteList">
              <div class="createSite" v-for="itemSite in addSiteCount" :key="itemSite">
                <p class="firstSiteP">
                  <span>
                    <i class="iconfont icon-zuobiao" style="display: inline-block"></i>
                    请指定签到地点
                  </span>
                  <em @click="delWeChatName">×</em>
                </p>
                <p class="secondSiteP">
                  <span class="range">
                    设置签到范围 （需要≥50米）
                   <font>500</font>
                  </span>
                  <span class="del">米<em @click="delWeChatName">×</em></span>
                </p>
              </div>
            </div>
            <p @click="addSignSite"><em>+</em> 继续添加可签到地点</p>
          </div>
        </li>
        <li>
          允许补签
          <span>
            <switch checked style="zoom: 0.5" color="#1a79c8" />
          </span>
        </li>
        <li>
          补签次数
          <number-box  />
        </li>
        <li>
          <p>允许其他人转发 <image src="/static/images/ask.png" alt=""></image></p>
        </li>
      </ul>
    </div>
    <div class="signQrcodeDiv">
      <p>确认即表示已同意《微信公众平台服务协议》</p>
      <button class="signQrcode">生成签到二维码</button>
    </div>
    <!-- 日期组件 -->
    <mask ref="testMask"
      top="0"
      :noclickhide='false'
      @onHideHander="onHideTestMask"
      @onShowHander="onShowTestMask">
      <activeModel :showActive="showActive">
        <Calendar
            :value="value"
            @select="select"
            ref="calendar"
        />
      </activeModel>
    </mask>
  </div>
</template>

<script>
// 引入日历插件
import Calendar from 'mpvue-calendar'
import "mpvue-calendar/src/style.css"
// 引入弹窗
import mask from '@/components/mask'
import activeModel from "@/components/activeModel"
// 引入计数器
import numberBox from "@/components/numbox"

export default {
  components:{
    Calendar,
    mask,
    activeModel,
    numberBox
  },
  data () {
    return {
      number: "1",
      minData:"1",
      maxData: "99",
      index:"0",
      days: ["全 天","自定义"],
      cur: 0,
      isShow: false, // 控制签到时间
      showActive: true, // 控制日历显示
      value: [2020,10,15],
      startDate: "",
      endDate: "",
      addTimeCount: 1,
      tHeight: "",
      isShowTime: false,
      isSelect: false,
      startTime: "00:00",
      endTime: "00:00",
      sHeight: "",
      isChecked: false,
      addSiteCount: 1
    }
  },
  methods: {
    retrunResult(e){
      console.log(e,'nsain');
    },
    selectType(i){
      this.cur = i;
      if(i == 1) {
        this.isShow = true;
        this.addTimeCount = 1;
        this.tHeight = "106px";
        this.isShowTime = true;
      }else{
        this.isShow = false;
        this.tHeight = "38px";
      }
    },
    changeStartTime(){
      this.$refs.testMask.showMask();
      this.isStart = true;
    },
    changeEndTime(){
      this.$refs.testMask.showMask();
      this.isStart = false;
    },
    onHideTestMask () {
      this.showActive = false
    },
    onShowTestMask () {
      let _this = this
      setTimeout(() => {
        _this.showActive = true
      }, 100)
    },
    select(val, val2) {
      // val 当前日期 数组  val2 对象
      if(this.isStart){
        this.startDate = val2.date;
      }else{
        this.endDate = val2.date;
      }
      this.$refs.testMask.hideMask();
    },
    addTimeSlot(){
      // 添加
      this.addTimeCount ++;
      this.tHeight = (106 + ((this.addTimeCount-1) * 46)) + "px";
    },
    delTimeSlot(){
      // 删除
      if(this.addTimeCount == 1){
        return false
      }
      this.addTimeCount -- ;
      let that = this;
      // 获取signTimeLi的高
      const query = wx.createSelectorQuery()
      query.select('#signTimeLi').boundingClientRect()
      query.exec(function(res){
        if(that.addTimeCount>1){
          that.tHeight = (res[0].height - 46) + "px";
        }else{
          that.tHeight = "106px";        
        }
      })
    },
    // getCurrentDomHeight( id, oldHeight, val, count, tHeight){
    //   const query = wx.createSelectorQuery();
    //   query.select(id).boundingClientRect();
    //   let height = "";
    //   query.exec(function(res){
    //     if(count > 1){
    //       tHeight = (res[0].height - val) + "px";
    //     } else {
    //       tHeight = oldHeight;        
    //     }
    //   })
    // },
    writeProject(){
      wx.navigateTo({
        url: "./project/main"
      });
    },
    selectStart(){
      // 选择开始时间
      this.isSelect = true;
    },
    selectEnd(){
      // 选择结束时间
      this.isSelect = false;
    },
    timeChange(e){
      let time = e.target.value;
      if(this.isSelect){
        this.startTime = time;
      }else{
        this.endTime = time;
      }
    },
    addSignSite(){
      // 添加可签到地点
      this.addSiteCount ++;
      let that = this;
      this.sHeight = (320 + ((this.addSiteCount-1) * 180)) + "rpx";
    },
    changeSignFlag(e){
      this.isChecked = e.mp.detail.value;
      this.addSiteCount = 1;
      if(this.isChecked && this.addSiteCount == 1){
         this.sHeight = "135px";
      }else{
         this.sHeight = "40px";
      }
    }
  },
}
</script>

<style lang="scss" scoped>
.createSign {
  width: 100%;
  .numberbox{
    width: 60px;
    height: 20px;
  }
  .projectList {
    position: relative;
    height: 160px;
    image {
      height: 100%;
    }
    .mask {
      position: absolute;
      left: 0;
      top: 0;
      bottom: 0;
      right: 0;
      background: rgba(0, 0, 0, 0.6);
    }
    button {
      width: 140px;
      height: 24px;
      position: absolute;
      left: 50%;
      top: 50%;
      margin-top: -12px;
      margin-left: -70px;
      z-index: 99;
      background: #fff;
      font-size: 10px;
      line-height: 25px;
      border-radius: 50px;
    }
  }
  .signRules {
    background: #fff;
    font-size: 14px;
    color: #000;
    font-weight: 600;
    padding: 0 10px;
    box-sizing: border-box;
    h6 {
      height: 30px;
      line-height: 30px;
    }
    > p {
      height: 30px;
      line-height: 30px;
    }
  }
}
.ruleInfo {
  li {
    border-top: 0.5px solid #eee;
    height: 40px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    > span {
      display: inline-block;
      i {
        display: inline-block;
        font-size: 10px;
        color: #666666;
      }
    }
    &:last-child {
      image {
        width: 15px;
        height: 15px;
      }
    }
  }
}
.signQrcodeDiv {
  height: 150px;
  text-align: center;
  background: #eeeeee;
  box-shadow: 0px -0.5px 0px 0px #eee;
  p {
    font-size: 12px;
    color: #666;
    line-height: 100px;
  }
  .signQrcode {
    width: 50%;
    margin-left: 25%;
    height: 30px;
    line-height: 30px;
    background: #199ed8;
    color: #fff;
    font-size: 12px;
  }
}
.signTimeLi {
  width: 100%;
  flex-direction: column;
  .timeSlot {
    border-top: 0.5px solid #eee;
    width: 100%;
    color: #666;
    font-size: 12px;
    .timeDiv {
      width: 100%;
      height: 55px;
      position: relative;
      > p {
        height: 30px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding-left: 15px;
        span {
          width: 56px;
          color: rgb(36, 33, 33);
          i {
            display: inline-block;
            font-size: 12px;
            padding-left: 3px;
          }
        }
      }
      .delicon{
        width: 10px;
        height: 10px;
        line-height: 8px;
        text-align: center;
        color: #fff;
        border-radius: 50%;
        background: red;
        font-size: 10px;
        position: absolute;
        left:0;
        top:10px;
      }
    }
    > p {
      height: 30px;
      display: flex;
      align-items: center;
      color: #199ed8;
      em {
        width: 12px;
        height: 12px;
        line-height: 11px;
        font-size: 12px;
        color: #fff;
        background: #199ed8;
        border-radius: 50%;
        text-align: center;
        margin-right: 8px;
      }
    }
  }
}
.signSite{
  flex-direction: column;
  .showSite{
    width: 100%;
    height: auto;
    >p{
        height: 30px;
        display: flex;
        align-items: center;
        color: #199ed8;
        em {
          width: 12px;
          height: 12px;
          line-height: 11px;
          font-size: 12px;
          color: #fff;
          background: #199ed8;
          border-radius: 50%;
          text-align: center;
          margin-right: 8px;
        }
    }
    .siteList{
      height: auto;
      .createSite{
        height: 90px;
        .firstSiteP,.secondSiteP{
          display: flex;
          justify-content: space-between;
          padding: 0 5px;
          box-sizing: border-box;
          align-items: center;
          height: 40px;
          color: #199ed8;
          em{
              width: 18px;
              height: 18px;
              line-height: 16px;
              text-align: center;
              font-size: 16px;
              color: #fff;
              background: #999;
              border-radius: 50%;
              box-sizing: border-box;
              display: inline-block;
              margin-left: 8px;
          }
        }
        .secondSiteP{
          .range{
            color: #666 !important;
            font{
              color: #000;
            }
          }
          .del{
            color: #000;
          }
        }
      }
    }
  }
}
.signSiteLeft{
  width: 100%;
  height: 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.signTimeLeft {
  width: 100%;
  height: 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.signTime {
  color: #666;
  font-size: 12px;
  i {
    border: 0.5px solid #999;
    margin-left: 10px;
    padding: .5px;
    display: inline-block;
    &.active {
      border-color: #199ed8;
      border-width: 1.5px;
    }
  }
}
</style>
