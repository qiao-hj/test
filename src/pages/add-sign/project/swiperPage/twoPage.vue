<!--  -->
<template>
  <div class="page-three">
      <div class="threeWay">
        <p>作业过程风险控制</p>
      </div>
      <div class="checkCont">
        <p> 安全综合控制措施:</p>
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
<style lang='scss' scoped>
.page-three{
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
  }
}
</style>