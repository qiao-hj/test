<!-- 修改个人信息 -->
<template>
  <div class="meansDiv">
      <ul class="meansList">
          <li>
              <label >修改头像</label>
              <div class="headPhoto">
                  <img :src="userInfo.avatarUrl" alt="">
                  <div class="mask">
                      <span>修改</span>
                  </div>
              </div>
          </li>
          <li>
              <label >名 字</label>
              <input type="text" v-model="userInfo.nickName" class="userName">
              <em @click="delWeChatName">×</em>
          </li>
          <li>
              <label >手机号</label>
              <input type="number" >
              <span class="autoWrite">自动填写</span>
          </li>
          <li>
              <label >微信号</label>
              <input type="text" placeholder="填写微信号" v-model="weChatNum">
              <em @click="delWeChatNum">×</em>
          </li>
          <li>
              <label >简 介</label>
              <input type="text" placeholder="填写简介信息" v-model="introMsg">
              <em @click="delIntroMsg">×</em>
          </li>
      </ul>
      <button class="saveBtn" @click="saveHandle">保 存</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
        userInfo: {},
        weChatNum: "",
        introMsg: "",
    };
  },
  methods:{
    delWeChatNum(){
      this.weChatNum = "";
    },
    delIntroMsg(){
      this.introMsg = "";
    },
    delWeChatName(){
      this.userInfo.nickName = "";
    },
    saveHandle(){
        let pages = getCurrentPages();
        let beforePage = pages[pages.length - 2];
        beforePage.setData({
            userInfo: this.userInfo,
            introMsg: this.introMsg
        })
        wx.navigateBack({
            delta: 1,
        })
    }
  },
  mounted(){
    this.userInfo = wx.getStorageSync("userInfo");
  }
}

</script>
<style lang='scss' scoped>
.meansDiv{
    height: 100%;
    background: #eeeeee;
}
.meansList{
    height: 240px;
    background: #ffffff;
    li{
        height: 40px;
        display: flex;
        padding: 0 10px;
        box-sizing: border-box;
        align-items: center;
        border-bottom: 1px solid #ccc;
        justify-content: space-between;
        &:first-child{
            height: 80px;
        }
        &:last-child{
            border-bottom: none;
        }
        label{
            font-size: 14px;
            font-weight: 600;
            width: 30%;
        }
        input{
            width: 60%;
            font-size: 12px;
            color: #666;
        }
        .userName{
            display: inline-block;
            width: 65%;
            font-size: 16px;
            font-weight: 600;
        }
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
        }
    }
    .headPhoto{
        width: 75%;
        position: relative;
        img{
          width: 60px;
          height: 60px;
        }
        .mask{
            width: 60px;
            height: 28px;
            background: rgba(0, 0, 0, 0.4);
            position: absolute;
            text-align: center;
            left: 0;
            bottom: 4px;
            span{
                height: 20px;
                line-height: 20px;
                color: #fff;
                font-size: 14px;
            }
        }
    }
    .autoWrite{
        width: 60px;
        height: 20px;
        text-align: center;
        background: #199ED8;
        color: #fff;
        font-size: 12px;
        border-radius: 3px;
        padding: 2px;
        box-sizing: border-box;
    }
}
.saveBtn{
    width: 90%;
    margin-left: 5%;
    height: 40px;
    line-height: 40px;
    color: #fff;
    font-size: 14px;
    margin-top: 30px;
    background: #199ED8;
}
</style>