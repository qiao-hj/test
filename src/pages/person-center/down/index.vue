<!-- 下载我的记录 -->
<template>
  <div class="downMyRecord">
     <img src="/static/images/down.png" alt="">
     <div>
         <input type="text" placeholder="请填写邮箱地址">
         <button>提交申请</button>
         <p>提示: 建议在整个签到活动结束后下载完整数据。单个签到每日只能申请一次。请勿重复提交。</p>
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
.downMyRecord{
    padding:0 10px;
    box-sizing: border-box;
    >img{
        height: 250px;
    }
    div{
        margin-top: 10px;
        input{
            width: 96%;
            margin-left: 2%;
            padding-left: 15px;
            box-sizing: border-box;
            border-radius: 5px;
            height: 40px;
            color: #666;
            background: #eee;
            font-size: 14px;
            border:0 ;
            outline: 0;
        }
        button{
            margin: 10px 0;
            width: 96%;
            height: 40px;
            line-height: 40px;
            font-size: 16px;
            margin-left: 2%;
            background: #199ed8;
            color: #fff;
        }
        p{
            width: 96%;
            margin-left: 2%;
            font-size: 14px;
            color: #999;
            line-height: 30px;
        }
    }
}
</style>