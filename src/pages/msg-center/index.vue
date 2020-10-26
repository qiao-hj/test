<!-- 信息中心  -->
<template>
  <div class="msgCenter">
    <div class="welcome">
      <div class="greeting">
         <img src="/static/images/kefu.jpg" alt="" class="img1">
         <div class="content">
          <div class="contentMain">
            <p>
              hi~你的工程签到通知中心已上线，后续关于小程序的功能更新，将会在这里告知大家哦~
            </p>
          </div>
          <p class="time">2018-12-29</p>
         </div>
      </div>
        <div class="contentList">
          <div class="greeting">
            <img src="/static/images/kefu.jpg" alt="" class="img1">
            <div class="content">
              <div class="section_net">
                <h3>工程签到使用介绍</h3>
                <div class="detail">
                  <p>
                    点这里, 查看工程签到常见使用问题
                  </p>
                  <img src="/static/images/1.jpg" alt="">
                </div>
              </div>
              <p class="time">2018-12-29</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
    };
  },
}

</script>
<style lang="scss" scoped>
.msgCenter{
  height: 100%;
  background: rgb(246, 242, 242);
  padding: 10px;
  box-sizing: border-box;
}
.welcome{
  .greeting{
    display: flex;
    .img1{
      background: #fff;
      padding: 7px;
      width: 15px;
      height: 15px;
      border-radius: 50%;
      margin-right: 20px;
    }
  }
  .content{
    width: 230px;
    .contentMain{ 
      height: 85px;
      background: #fff;
      border-radius: 8px;
      p{
        width: 180px;
        padding: 10px;
        font-size: 14px;
        font-weight: 600;
        height: 20px;
        line-height: 20px;
      }
    }
  }
  .time{
    height: 40px;
    line-height: 40px;
    font-size: 12px;
    color: #666;
  }
}
.section_net{
  background: #fff;
  height: 95px;
  h3{
    font-size: 14px;
    padding-left: 10px;
    height: 35px;
    line-height: 35px;
    font-weight: 600;
  }
  .detail{
    display: flex;
    align-items: center;
    margin: 0 10px;
    border-bottom: 1.5px solid #ccc;
    p{
      width: 85%;
      color: #999;
      font-size: 12px;
    }
    img{
      padding-left: 20px;
      width: 50px;
      height: 50px;
    }
  }
}
</style>