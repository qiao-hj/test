<!--  -->
<template>
  <div class="page-four">
      <div class="checkCont">
        <p> 现场风险复测变化情况及补充控制措施:</p>
        <textarea :value="textAreaValue" class='text_area' cols="100%" rows="10" ></textarea>
      </div>
      <button size="mini" class="submit">提 交</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
        textAreaValue: ""
    };
  },
}

</script>
<style lang='scss' scoped>
.page-four{
  padding: 0 10px;
  box-sizing: border-box;
  text-align: center;
}
.checkCont{
  >p{
    font-size: 14px;
    height: 40px;
    line-height: 40px;
    color: #1296db;
    font-weight: 600;
  }
  .text_area{
      width: 90%;
      height: 100px;
      border: .1px solid #ccc;
  }
}
.submit{
    background: #1296db;
    color: #fff;
    margin-top: 30px;
}
</style>