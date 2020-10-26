<!-- 个人中心 -->
<template>
  <div>
    <div class="centerTop">
       <div class="userCenter">
         <div class="userLeft">
           <img :src="userInfo.avatarUrl" alt="">
          <p class="userDetail">
            <span>{{userInfo.nickName}}</span>
            <b>简介: {{introMsg}}</b>
          </p>
         </div>
          <span class="editMeans" @click="editMeans">编辑资料</span>
       </div>
      <ol class="signRecord">
        <li>
          <i>73</i>
          <span>累计签到</span>
        </li>
        <li>
          <i>26</i>
          <span>连续签到</span>
        </li>
        <li>
          <i>73</i>
          <span>最大连续</span>
        </li>
      </ol>
    </div>
    <div class="lineDiv"></div>
    <ul class="ulsList">
      <li v-for="(item,ind) in listData" :key="ind" @click="arrowsHandle(ind)">
        <span>
          <b :class="'iconfont '+ item.icon "></b>
          {{item.title}}
        </span>
        <i class="iconfont icon-left" v-if="ind != 3"></i>
      </li>
    </ul>
    <mask 
      ref="testMask"
      top="0"
      @onHideHander="onHideTestMask"
      @onShowHander="onShowTestMask">
      <div class="mask">
          <div class="top">
            <img src="/static/images/kefu.jpg" alt="">
            <span>工程签到</span>
            <i class="iconfont icon-left"></i>
          </div>
          <ul>
              <li>
                <i class="iconfont icon-fasonggeipengyou"></i>
                <span>发送给朋友</span>
              </li>
              <li>
                <i class="iconfont icon-pengyouquan"></i>
                <span>分享到朋友圈</span>
              </li>
              <li>
                <i class="iconfont icon-shoucang"></i>
                <span>收藏</span>
              </li>
              <li>
                <i class="iconfont icon-method-draw-image"></i>
                <span>添加到我的小程序</span>
              </li>
              <li>
                <i class="iconfont icon-changfangxingfengmian_huaban1"></i>
                <span>添加到桌面</span>
              </li>
          </ul>
          <ul>
             <li>
                <i class="iconfont icon-bianzu"></i>
                <span>浮窗</span>
              </li>
              <li>
                <i class="iconfont icon-shezhi"></i>
                <span>设置</span>
              </li>
              <li>
                <i class="iconfont icon-tousu"></i>
                <span>反馈与投诉</span>
              </li>
              <li>
                <i class="iconfont icon-shuaxin"></i>
                <span>重新进入小程序</span>
              </li>
              <li>
                <i class="iconfont icon-shumiao-"></i>
                <span>成长守护防沉迷</span>
              </li>
          </ul>
          <button @click="cancelHandle">取 消</button>
      </div>
    </mask>
  </div>
</template>

<script>
import mask from "@/components/mask"

export default {
  components: {
    mask
  },
  data () {
    return {
      listData: [{
        title: "帮助中心",
        icon: "icon-bangzhuzhongxin"
      },{
        title: "清除缓存",
        icon: "icon-icon_qingchuhuancunx"
      },{
        title: "下载我的记录",
        icon: "icon-xiazai"
      },{
        title: "电脑端",
        icon: "icon-diannaoduanfangwen"
      },{
        title: "添加到我的小程序",
        icon: "icon-xiaochengxu"
      }],
      userInfo: {},
      introMsg: "",
      visible: false,
      showActive: false
    };
  },
  onLoad () {
    this.userInfo = wx.getStorageSync('userInfo');
    console.log(this.userInfo,'---');
  },
  onShow() {
    let pages = getCurrentPages();
    let currPage = pages[pages.length - 1]; //当前页面
    if(currPage && currPage.data.userInfo){
      this.userInfo = currPage.data.userInfo;
      this.introMsg = currPage.data.introMsg;
    }
  },
  methods: {
    onHideTestMask () {
      this.showActive = false
    },
    onShowTestMask () {
      let _this = this
      setTimeout(() => {
          _this.showActive = true
      }, 100)
    },
    showMask(){
      this.$refs.testMask.showMask();
    },
    arrowsHandle(ind){
      if(ind == 0){
        wx.navigateTo({
          url: "./help/main"
        })
      }else if(ind == 1){
        wx.showToast({
            title: "清除成功", 
            icon: 'success',
            duration: 3000, 
            mask: true, 
        });
      }else if(ind == 2){
        wx.navigateTo({
          url: "./down/main"
        })
      }else if(ind == 3){

      }else if(ind == 4){
        this.showMask()
      }
    },
    editMeans(){
       wx.navigateTo({
          url: "./means/main"
        })
    },
    cancelHandle(){
       this.$refs.testMask.hideMask();
    }
  },
}

</script>
<style lang="scss" scoped>
.centerTop{
  height:200px;
  .userCenter{
    height: 120px;
  }
  .signRecord{
    height: 80px;
    border-top: 1px solid #eee;
    display: flex;
    align-items: center;
    font-weight: 600;
    li{
      flex:1;
      font-size: 14px;
      color: #666;
      text-align: center;
      span{
        display: block;
        color: #999;
      }
    }
  }
}
.userCenter{
  display: flex;
  justify-content: space-between;
  padding: 0 20px;
  box-sizing: border-box;
  align-items: center;
  .userLeft{
    display: flex;
    align-items: center;
    img{
      width: 50px;
      height: 50px;
      border-radius: 50%;
    }
    .userDetail{
      font-size: 12px;
      margin-left: 10px;
      span{
        font-size: 16px;
        line-height: 12px;
      }
    }
  }
  .editMeans{
    width: 60px;
    height: 20px;
    border: 2px solid #000;
    border-radius: 8px;
    text-align: center;
    line-height: 20px;
    font-size: 12px;
  }
}
.lineDiv{
  width: 100%;
  height: 10px;
  background: #eee;
  margin-bottom: 25px;
}
.ulsList li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 15px;
  box-sizing: border-box;
  height: 40px;
  span {
    font-weight: 600;
    font-size: 14px;
    b {
      display: inline-block;
      font-size: 16px;
      padding-right: 8px;
    }
  }
  &:nth-child(2) {
    b {
      width: 20px;
      height: 14px;
      font-size: 25px;
      margin-left: -5px;
    }
  }
  &:nth-child(3) {
    b {
      width: 20px;
      height: 13px;
      font-size: 30px;
      margin-left: -8px;
    }
  }
  &:nth-child(5) {
    b {
      font-size: 18px;
    }
  }
  i {
    font-size: 14px;
    color: #999999;
  }
}
.mask{
  position: absolute;
  width: 100%;
  height: 60%;
  bottom: 0;
  transition: all 0.3s;
  background-color: #fafafa;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  .top{
    display: flex;
    height: 60px;
    align-items: center;
    padding:0 10px;
    box-sizing: border-box;
    image{
      background: #fff;
      padding: 7px;
      width: 15px;
      height: 15px;
      border-radius: 50%;
      margin-right: 20px;
    }
    span{
      font-size: 14px;
    }
    i{
      font-size: 20px;
      padding-left: 8px;
    }
  }
  ul{
    display: flex;
    height: 110px;
    align-items: flex-start;
    border-top: .5px solid #ccc;
    li{
      cursor: pointer;
      text-align: center;
      color: #999;
      flex: 1;
      padding-top: 25px;
      i{
        display: inline-block;
        font-size: 20px;
        width: 40px;
        height: 40px;
        background: #fff;
        border-radius: 8px;
        line-height: 40px;
        color: #199ED8;
      }
      span{
        display: block;
        font-size: 12px;
        color: #666;
        margin-top: 7px;
      }
    }
  }
  button{
    background: #fff;
    width: 100%;
    height: 40px;
    line-height: 40px;
    font-size: 14px;
    border-bottom-left-radius: 0;
    border-bottom-right-radius: 0;
    border: none;
    outline: none;
  }
}
</style>