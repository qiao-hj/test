<!-- 修改个人信息 -->
<template>
  <div class="meansDiv">
      <ul class="meansList">
          <li>
              <label >头像</label>
              <div class="headPhoto">
                  <img :src="userInfo.avatarUrl" alt="">
              </div>
          </li>
          <li>
              <label >名 字</label>
              <input type="text" v-model="queryParams.nickName" class="userName">
          </li>
          <li>
              <label >手机号</label>
              <input type="number" v-model="queryParams.phoneNumber" @blur="checkPhone">
              <span class="autoWrite">自动填写</span>
          </li>
          <li>
              <label>手写名字</label>
              <div type="textarea" @click="handleBlur" class="signHandle">{{queryParams.signName}}</div>
          </li>
      </ul>
      <button class="saveBtn" @click="submitHandle">提 交</button>
     <!-- 手写名字 -->
     <mask 
      ref="testMask"
      top="0"
      @onHideHander="onHideTestMask"
      @onShowHander="onShowTestMask">
      <div class="mask">
          <div class="top">
            <button @click="cancelHandle">取 消</button><button @click="sureHandle">确 定</button>
          </div>
          <input type="text" class="signBox" v-model="writeName">
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
        userInfo: {},
        queryParams: {
          nickName: "",
          phoneNumber: "",
          signName: "",
        },
        writeName: "",
    };
  },
  methods:{
    checkPhone(){
      let reg = /^1[0-9]{10}$/;
      if(!(reg.test(this.queryParams.phoneNumber))){ 
          wx.showToast({
            title: '请输入正确的手机号',
            icon:'none'
          })
          return false; 
      } 
    },
    submitHandle(){
      let msg = this.queryParams.nickName && this.queryParams.phoneNumber && this.queryParams.signName; 
      if(!msg){
        wx.showToast({
          title: '请把信息补充完整',
          icon:'none'
        })
        return false;
      }else{
        let reg = /^1[0-9]{10}$/;
        if(!(reg.test(this.queryParams.phoneNumber))){ 
            wx.showToast({
              title: '请输入正确的手机号',
              icon:'none'
            })
            return false; 
        }else{
          wx.navigateTo({
            url: "./signsuccess/main"
          })  
        }
      }    
    },
    handleBlur(){
      this.$refs.testMask.showMask();
    },
    sureHandle(){
      this.queryParams.signName = this.writeName;
      this.$refs.testMask.hideMask();
    },
    cancelHandle(){
      this.$refs.testMask.hideMask();
    },
  },
  mounted(){
    this.userInfo = wx.getStorageSync("userInfo");
  }
}

</script>
<style lang='scss' scoped>
.meansDiv{
    height: 100%;
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
.signHandle{
    width: 90%;
    height: 100px;
    line-height: 60px;
    font-size: 50px;
    font-weight: 600;
    margin-top: 70px;
}
.mask{
  position: absolute;
  width: 90%;
  height: 30%;
  bottom: 47%;
  left: 5%;
  transition: all 0.3s;
  background-color: #fafafa;
  .top{
      display: flex;
      height: 40px;
      margin-top: 10px;
    button{
        height: 30px;
        line-height: 30px;
        font-size: 14px;
        border-radius: 10px;
        &:last-child{
            background: #199ED8;
            color: #fff;
        }
    }
  }
  .signBox{
      border:.5px solid #ccc;
      width: 300px;
      height: 100px;
      margin-left: 20px;
      padding-left: 5px;
  }
}
</style>