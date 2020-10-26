<!-- 计数器 -->
<template>
    <div class='num-box'>
        <div class="minus-num" @click='minusNumber'>-</div>
        <div class='number'><input type="number" @change="inputBlur" v-model="number" /></div>
        <div class="plus-num" @click='plusNumber'>+</div>
    </div>
</template>

<script>
export default {
  data () {
    return {
        number: 1
    };
  },
  methods: {
    minusNumber(){
      this.number--;
      if(this.number <= 1 ){
        wx.showToast({
          title: '不能再减少了！',
          icon:'none'
        })
        this.number = 1;
      }
      this.$emit('numberBoxChange', this.number)
    },
    plusNumber(){
      this.number++;
      if(this.number >= 100){
        wx.showToast({
          title: '不能再增加了！',
          icon:'none'
        })
        this.number = 100;
      }
      this.$emit('numberBoxChange', this.number)
    },
    inputBlur(e){
      let reg = /[0-9]*[1-9][0-9]*/; 
      if(reg.test(this.number)){
        this.number = e.target.value;
      }else{
        wx.showToast({
          title: '请输入数字！',
          icon:'none'
        })
        this.number = "";
      }
      this.$emit('numberBoxChange', this.number)
    }
  }
}

</script>
<style lang='scss' scoped>
.num-box {
  width: 90px;
  height: 30px;
  border: 1px solid #ebeef5;
  border-radius: 8px;
  display: flex;
  box-sizing: border-box;
}
.minus-num, .plus-num {
  width: 40px;
  line-height: 30px;
  font-size: 16px;
  text-align: center;
}
.minus-num{
  border-right: .5px solid #ebeef5;
}
.plus-num{
  border-left: .5px solid #ebeef5;
}
.number {
  width: 30px;
  height: 30px;
}
.num-box .number input {
  width: 30px;
  height: 30px;
  line-height: 35px;
  text-align: center;
  font-size: 14px;
  color: #333;
}
</style>