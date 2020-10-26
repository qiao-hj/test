<!--  -->
<template>
  <div class="recordBox">
    <p>每日站班会及风险控制措施检查记录表</p>
    <ul class="recordList">
        <li v-for="(item,ind) in paramsData" :key="ind">
            <span>{{item.text}}: </span>
            <input type="text" class="inputText">
        </li>
    </ul> 
  </div>
</template>

<script>
export default {
  data () {
    return {
        paramsData:[{
            text: "作业票号",
            value: ""
        },{
            text: "工程名称",
            value: ""
        },{
            text: "作业部位及内容",
            value: ""
        },{
            text: "工程负责人",
            value: ""
        },{
            text: "安全监护人",
            value: ""
        },{
            text: "施工机具",
            value: ""
        },{
            text: "当日风险等级",
            value: ""
        },{
            text: "备注",
            value: ""
        }]
    };
  },
}

</script>
<style lang='scss' scoped>
.recordBox{
    padding: 0 8px;
    >p{
        font-weight: 600;
        color: #199ED8;
        font-size: 16px;
        padding-left: 5px;
    }
}
.recordList{
    li{
        height: 40px;
        line-height: 40px;
        border-bottom: .5px solid #ccc;
        span{
            display: inline-block;
            color: #199ED8;
            font-weight: 600;
            font-size: 12px;
        }
        input{
            float: right;
            border: 0;
            outline: 0;
            width: 80%;
            height: 40px;
            font-size: 12px;
        }
    }
}
</style>