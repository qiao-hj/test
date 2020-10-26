<!--  -->
<template>
  <div class="five-page">
    <div class="threeWay">
    <!-- 三交 -->
    <p>现场风险复测变化情况及补充控制措施: </p>
    </div>
    <div class="checkCont">
    <!-- 检查内容 -->
    <p> 备注:</p>
    
    </div>
    <div class="readRadio">
        <label class="radio-group" style="line-height:30px">
            <input v-model="radioVal" type="radio" value="我已认真阅读" @change="radioChange" style="zoom:0.5"> <a href="#">我已认真阅读</a>
        </label>
        <button class="goSignBtn" @click="goSignPage">进入签到</button>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
        checked: true,
        radioVal: 0
    };
  },
  methods: {
      radioChange(val){
        console.log(val,'val==');
      }
  },
}

</script>
<style lang='scss' scoped>
.five-page{
    padding:0 10px;
    box-sizing: border-box;
}
.readRadio{
  width: 100%;
  position: absolute;
  bottom: 15%;
  font-size: 14px;
  color: #199ED8;
  text-align: center;
  .radio-group{
    display: flex;
    justify-content: center;
  }
  .goSignBtn{
      width: 50%;
      margin-left: 25%;
      margin-top: 20px;
      height: 30px;
      line-height: 30px;
      background: #199ED8;
      font-size: 14px;
      color: #fff;
  }
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
  }
}
</style>