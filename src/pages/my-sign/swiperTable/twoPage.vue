<!--  -->
<template>
  <div class="page-two">
      <div class="threeWay">
        <!-- 三交 -->
        <p> 三交: <img src="/static/icon/user.png" alt=""></p>
        <ul class="threeWayList">
          <li v-for="(itemWay,ind) in paramsData" :key="ind">{{itemWay.text}}:
            <span>内容</span>
          </li>
        </ul>
      </div>
      <div class="checkCont">
        <!-- 检查内容 -->
        <p> 检查内容: <img src="/static/icon/file.png" alt=""></p>
        <ul class="checkContList">
          <li>三查 (查衣着、查三宝、查精神状态)、查作业必备条件:</li>
          <li>
            当日风险控制措施:
          </li>
        </ul>
      </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      paramsData:[{
            text: "交任务",
            value: ""
        },{
            text: "交安全",
            value: ""
        },{
            text: "交技术",
            value: ""
        }]
    };
  },
}

</script>
<style lang='scss' scoped>
.page-two{
  padding: 0 10px;
  box-sizing: border-box;
}
.threeWay, .checkCont{
  >p{
    display: flex;
    align-items: center;
    font-size: 14px;
    height: 40px;
    vertical-align:middle;
    color: #1296db;
    font-weight: 600;
    img{
      width: 25px;
      height:25px;
      padding-left: 10px;
    }
  }
}
.checkCont{
  margin-top: 30px;
}
.threeWayList,.checkContList{
  li{
    height: 30px;
    line-height: 30px;
    font-weight: 600;
    color: #1296db;
    font-size: 14px;
    border-bottom: .5px solid #ccc;
  }
}
</style>