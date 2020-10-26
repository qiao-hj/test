<!-- 签到成功 -->
<template>
  <div class="signBox">
      <img src="/static/images/sign.jpg" alt="">
      <p>恭 喜 你 签 到 成 功</p>
      <span>你已坚持签到{{signCount}}次</span>
  </div>
</template>

<script>
export default {
  data () {
    return {
        signCount: 1
    };
  },
  onUnload(){
    // 监听页面卸载事件
    console.log('返回');
    wx.redirectTo({
      url: '/pages/my-sign/main',
    })
  },
}

</script>
<style lang='scss' scoped>
.signBox{
    height: 280px;
    text-align: center;
    border-bottom: .5px solid #eee;
    img{
        width: 300px;
        height: 140px;
    }
    p{
        margin-top: 10px;
        font-size: 16px;
        font-weight: 600;
        color: #666;
    }
    span{
        font-size: 10px;
        font-weight: 600;
        color: #999;
    }
}
</style>