<!-- 扫码签到 -->
<template>
  <div class="scanSignDiv">
      <div class="scanTop">
        <img src="/static/images/ticket.jpg" alt="">
        <div class="signTit">
            <p class="title">{{title}}</p>
            <!-- <p class="time">今日签到已在{{time}}完成</p> -->
            <button class="signBtn" @click="signHandle">签 到</button>
            <div class="date-progess">
                <p class="progess"> 
                    <span class="day">
                        第{{beginDay}}天/{{allDay}}天
                    </span>
                    <span class="personCount">共{{sum}}人参与</span>
                </p>
                <progress :percent="percent" activeColor="#EA5A49"/>
            </div>
        </div>
      </div>
     <div class="scanBot">
        <h5 class="titUser">
            <i class="iconfont icon-yonghu"></i>
            <span>{{userName}}</span>
            <b>发起人</b>
        </h5>
        <div class="rulesBot">
            <button class="lookBtn" size="mini" @click="lookProject">点击查看工程单</button>
            <div class="descText">
                <p><i class="iconfont icon-guize"></i> 签到规则</p>
                <ol class="ruleItems">
                    <li>
                        <i class="iconfont icon-wujiaoxing"></i>
                        签到日期: 2020-09-22 至 2021-09-21
                    </li>
                    <li>
                        <i class="iconfont icon-wujiaoxing"></i>
                        每日 可签到时间: 00:00 至 23:59
                    </li>
                    <li>
                        <i class="iconfont icon-wujiaoxing"></i>
                        签到规则:
                        <br>
                        微信 「扫一扫」扫描二维码即可参与签到
                    </li>
                </ol>
            </div>
            <ul class="handleList">
                <li v-for="(items,n) in handleList" :key="n" @click="typeHandle(n)">
                    <i :class="'iconfont '+ items.icon"></i>
                    {{items.tit}}
                </li>
            </ul>
        </div>
        <mask 
            ref="testMask"
            top="0"
            @onHideHander="onHideTestMask"
            @onShowHander="onShowTestMask">
            <div class="mask">
                <p>选择分享方式</p>
                <ul class="shareList">
                    <li>
                        <i class="iconfont icon-ziyuan"></i>
                        <span>微信好友</span>
                    </li>
                    <li>
                        <i class="iconfont icon-xiaochengxuma"></i>
                        <span>签到小程序码</span>
                    </li>
                    <li>
                        <i class="iconfont icon-erweima"></i>
                        <span>签到二维码</span>
                    </li>
                </ul>
                <button @click="cancelHandle">取 消</button>
            </div>
        </mask>
        <mask 
            ref="testMask1"
            top="0"
            @onHideHander="onHideTestMask"
            @onShowHander="onShowTestMask">
            <div class="mask1">
                <div class="top">
                    <img src="/static/images/kefu.jpg" alt="">
                    <span>工程签到</span>
                    <i>申请</i>
                </div>
                <h3>获取你的位置信息</h3>
                <p style="text-align:left">你的位置信息将用于判断签到范围</p>
                <div class="buttonList">
                    <button @click="cancelHandle">拒 绝</button>
                    <button @click="sureHandle">允 许</button>
                </div>
            </div>
        </mask>
     </div>
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
        title: "侯马10kV上马线东阳呈支线改造工程",
        time: "09:22",
        userName: "快乐星球持证驾驶员",
        handleList: [{
            icon: "icon-xiugai",
            tit: "修改"
        },{
            icon: "icon-fenxiang",
            tit: "分享"
        },{
            icon: "icon-tongji",
            tit: "统计"
        },{
            icon: "icon-dayin",
            tit: "打印"
        }],
        percent: "1",
        beginDay: 1,
        allDay: 365,
        sum: 14,
        showActive: false
    };
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
      lookProject(){
        getApp().globalData.isSign = true;
        wx.switchTab({
            url: "/pages/my-sign/main"
        })
      },
      showMask(){
        this.$refs.testMask.showMask();
      },
      typeHandle(n){
          switch(n){
            case 0:
                wx.switchTab({
                    url: "/pages/add-sign/main"
                })
            break;
            case 1:
                this.showMask();
            break;
            case 2:
                wx.navigateTo({
                    url: "./statistics/main"
                })
            break;
            case 3:
                
            break;
            default:;
          }
      },
      cancelHandle(){
          this.$refs.testMask.hideMask();
      },
      signHandle(){
           // 签到事件
           this.$refs.testMask1.showMask();
      },
      sureHandle(){
        // 允许
        wx.navigateTo({
            url: "./signmsg/main"
        })
      }
  }
}

</script>
<style lang='scss' scoped>
.scanSignDiv{
 height: 100%;
 background: #3834341f;
}
.scanTop{
    height: 150px;
    img{
      width: 100%;
      height: 150px;
      position: relative;
      &:before{
        content: "";
        display: inline-block;
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        height: 150px;
        background: rgba(0, 0, 0, 0.6);
     }
    }
    .signTit{
        width:100%;
        height: 150px;
        text-align: center;
        position: fixed;
        top: 30px;
        left: 0;
        color: #fff;
        line-height: 30px;
        .title{
            font-size: 16px;
            font-weight: 600;
        }
        .time{
            font-size: 14px;
        }
        .signBtn{
            width: 50%;
            height: 25px;
            line-height: 25px;
            margin-left: 25%;
            font-size: 14px;
            color: #fff;
            background: #199ED8;
            margin-top: 3px;
        }
    }
    .date-progess{
        width: 90%;
        margin-left: 5%;
        margin-top: 20px;
        .progess{
          display: flex;
          justify-content: space-between;
          color: #fff;
          font-size: 14px;
        }
    }
}
.scanBot{
    height: 320px;
    background: #fff;
    padding-top: 10px;
}
.titUser{
    height: 40px;
    display: flex;
    align-items: center;
    padding: 0 10px;
    box-sizing: border-box;
    border-bottom: 1px solid #cccccc;
    i{
        width:15px;
        height: 15px;
    }
    span{
        font-size: 16px;
        padding: 5px;
    }
    b{
        padding:3px;
        font-weight: 600;
        text-align: center;
        background:#d4929e;
        color: #fff;
        font-size: 10px;
        border-radius: 3px;
        margin-bottom: 2px;
    }
}
.rulesBot{
    padding: 15px;
    box-sizing: border-box;
    .descText{
        >p{
            font-size: 16px;
            height: 30px;
            line-height: 30px;
            font-weight: 600;
            i{
                font-size: 10px;
                display: inline-block;
                padding-right: 10px;
            }
        }
    }
    
    .lookBtn{
       height: 25px;
       line-height: 25px;
       font-size: 12px;
       color: #fff;
       background: #199ED8;
       border-radius: 50px;
       width:150px;
       margin: 3px 0;
    }
}
.ruleItems{
    li{
        font-size: 14px;
        color: #666;
        line-height: 25px;
        i{
            font-size: 6px;
            display: inline-block;
            padding-right: 5px;
        }
    }
}
.handleList{
    display: flex;
    align-items: center;
    margin-top: 25px;
    li{
        flex: 1;
        text-align: center;
        color: #999;
        font-size: 14px;
        i{
            display: block;
            color: #199ED8;
            padding-bottom: 2px;
        }
    }
}
.mask {
  position: absolute;
  width: 100%;
  height: 30%;
  bottom: 0;
  transition: all 0.3s;
  background-color: #fff;
  p{
      width: 100%;
      text-align: center;
      height: 40px;
      line-height: 40px;
      font-size: 14px;
    }
  .shareList{
      width: 100%;
      display: flex;
      align-items: center;
      li{
          flex:1;
          text-align: center;
          i{
              font-size: 25px;
              color: #199ED8;
              display: block;
          }
          span{
              font-size: 14px;
          }
      }
  }
  button{
        height: 40px;
        line-height: 40px;
        margin-top: 40px;
        width:100%;
        background: #eee;
        font-size: 14px;
        border: 0;
    }
}
.mask1{
  position: absolute;
  width: 100%;
  height: 40%;
  bottom: 0;
  transition: all 0.3s;
  background-color: #fafafa;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  padding:0 10px;
  box-sizing: border-box;
  .top{
    display: flex;
    height: 60px;
    align-items: center;
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
      font-size: 14px;
      padding-left: 8px;
      color: #999;
    }
  }
  h3{
      font-weight: 600;
      font-size: 18px;
      height: 30px;
      line-height: 30px;
  }
  >p{
      color: #999;
      font-weight: 600;
  }
  .buttonList{
      display: flex;
      justify-content: space-around;
  }
  button{
    margin-top: 20px;
    width: 30%;
    height: 40px;
    line-height: 40px;
    font-size: 14px;
    border: none;
    outline: none;
    font-weight: 600;
    &:first-child{
      background: #eee;
    }
    &:last-child{
      background: green;
      color: #fff;
    }
  }
}
</style>