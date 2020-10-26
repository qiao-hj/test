<!-- 统计 -->
<template>
  <div class="statisticsDiv">
    <div class="searchBox">
      <div class="searchLeft">
        <span @click="changeHandle">{{searchVal.text}}<i :class="'iconfont '+searchVal.icon"></i><i :class="isdown ? 'iconfont icon-down' : 'iconfont icon-up'"></i></span>
        <ul class="selectList"  :class="{'active': isdown}" >
            <li v-for="(item, ind) in option" :key="ind" @click="changeValue(item)"><a herf="#">{{item.text}}</a><i :class="'iconfont '+item.icon"></i> </li>
        </ul>
      </div>
      <div class="searchRight">
         <input type="text" class="searchInput">
         <button size="mini" class="searchBtn">搜索</button>
      </div>
    </div>
    <div class="searchResult">
      <div class="useResult" v-show="searchVal.value == 1">
        <!-- 按姓名 -->
        <p>姓 名: 李方军</p>
        <p>电 话: 13094802713</p>
        <div>
           <ol class="signRecord">
              <li>
                <i>12</i>
                <span>出勤天数</span>
              </li>
              <li>
                <i>5</i>
                <span>缺勤天数</span>
              </li>
              <li>
                <i>12</i>
                <span>连续签到</span>
              </li>
            </ol>
        </div>
        <div class="calendarDiv">
          <Calendar />
        </div>
        <p>作业内容: </p>
        <p>电缆铺设:</p>
        <div class="cableLay">
          <progress :percent="percent" activeColor="green" class="progress" />14天
        </div>
      </div>
      <div class="dateResult" v-show="searchVal.value == 0">
        <ul class="dataList">
          <li>日 期: 2020年9月22日</li>
          <li>工程名称: 侯马10kV上马线东阳呈支线改造工程</li>
          <li>第16天(16/60)</li>
          <li>工程负责人: 李方军</li>
          <li>安全监护人: 冯海东</li>
          <li>出勤人数: 25人</li>
          <li>迟到人数: 5人</li>
          <li>风险措施: </li>
        </ul>
        <div class="cableLay1">
          <progress :percent="percent1" activeColor="green" class="progress" />21天
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// 引入日历插件
import Calendar from "@/components/date.vue"

export default {
  components: {
    Calendar
  },
  data () {
    return {
      isdown: false,
      searchVal:  { 
        text: "姓 名", 
        value: 0, 
        icon: "icon-yonghu" 
      },
      option: [
        { 
          text: "姓 名", 
          value: 0, 
          icon: "icon-yonghu" 
        },
        { 
          text: "日 期", 
          value: 1, 
          icon: "icon-riqi" 
        },
      ],
      percent: "7",
      dataList: [{
        text: "z`"
      }],
      percent1: "7"
    }
  },
  methods: {
    changeHandle(){
      this.isdown = !this.isdown;
    },
    changeValue(e){
      this.searchVal = e;
      this.isdown = !this.isdown;
    }
  }
}

</script>
<style lang='scss' scoped>
.statisticsDiv {
  width: 100%;
  padding: 5px 30px;
  box-sizing: border-box;
  .searchBox {
    display: flex;
    height: 40px;
    font-size: 14px;
  }
  .searchLeft {
    width: 80px;
    text-align: center;
    i {
      display: inline-block;
      font-size: 14px;
      font-weight: 600;
      padding-left: 3px;
    }
  }
  .selectList {
    width: 60px;
    height: 40px;
    text-align: right;
    display: none;
    li {
      height: 25px;
      line-height: 25px;
      a {
        display: inline-block;
      }
    }
    &.active {
      display: block;
    }
  }
  .searchRight {
    width: 250px;
    height: 25px;
    display: flex;
    position: relative;
    .searchInput {
      width: 200px;
      height: 25px;
      border: 0.1px solid #ccc;
      font-size: 12px;
      border-radius: 50px;
      padding-left: 2px;
    }
    .searchBtn {
      height: 27px;
      color: #fff;
      background: #199ed8;
      font-size: 12px;
      border-radius: 50px;
      position: absolute;
      right: 30px;
      top: 0px;
    }
  }
  .searchResult{
    margin-top: 20px;
    padding: 0 10px;
    box-sizing: border-box;
    .useResult{
      p{
        height: 30px;
        line-height: 30px;
        font-size: 12px;
        color: #666;
        font-weight: 600;
      }
     
    }
  }
  .signRecord{
    height: 50px;
    display: flex;
    align-items: center;
    font-weight: 600;
    li{
      flex:1;
      font-size: 12px;
      color: #666;
      text-align: center;
      span{
        padding-top: 5px;
        display: block;
      }
    }
  }
  .cableLay{
    font-size: 14px;
    color: #666;
    display: flex;
    align-items: center;
  }
  .progress{
    width: 80%;
    padding-left: 10px;
    padding-right: 10px;
    height: 30px;
    border-radius: 50px;
  }
  .calendarDiv{
    border: .5px solid #eee;
    margin: 5px 0 ;
  }
  .dataList{
    li{
      height: 30px;
      line-height: 30px;
      font-size: 14px;
      font-weight: 600;
      color: #666;
    }
  }
  .cableLay1{
    font-size: 14px;
    color: #666;
    display: flex;
    align-items: center;
  }
}
</style>