<!-- 日历 -->
<template>
  <div class="calendarBox">
    <!-- 日历年月 -->
    <div class='calendar_title'>
        <i class="iconfont icon-left1"  @click="lastMonth"></i>
        <a>{{data.year}}年{{data.month}}月</a>
        <i class='iconfont icon-left' @click="nextMonth"></i>
    </div>

    <!-- 日历主体 -->
    <div class='calendar'>
        <div class='header'>
            <div v-for='(item, ind ) in data.date' :key='ind' :class='(index == todayIndex) && isTodayWeek ? "weekMark" : ""'>{{item}}
               <div></div>
            </div>
        </div>

        <div class='date-box'>
            <block v-for='(dateitem, key) in data.dateArr' :key='key'>
                <div :class='data.isToday == dateitem.isToday ? "nowDay" : ""'>
                    <div class='date-head' @click='lookHuoDong' :data-year='data.year' :data-month='data.month' :data-datenum='dateitem.dateNum'>
                        <div>{{dateitem.dateNum}}</div>
                    </div>
                </div>
            </block>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return{
        data: {
            year: 0,
            month: 0,
            isToday: 0,
            date: ['周日', '周一', '周二', '周三', '周四', '周五', '周六'],
            dateArr: [],
            isTodayWeek: false,
            todayIndex: 0
        }   
    }
  },
  onLoad() {
    let now = new Date();
    let year = now.getFullYear();
    let month = now.getMonth() + 1;
    this.dateInit();
    this.data.year = year;
    this.data.month = month;
    this.data.isToday = '' + year + month + now.getDate();
  },
  methods: {
    dateInit(setYear, setMonth) {
        //全部时间的月份都是按0~11基准，显示月份才+1
        let dateArr = [];                       //需要遍历的日历数组数据
        let arrLen = 0;                         //dateArr的数组长度
        let now = setYear ? new Date(setYear, setMonth) : new Date();
        let year = setYear || now.getFullYear();
        let nextYear = 0;
        let month = setMonth || now.getMonth();                 //没有+1方便后面计算当月总天数
        let nextMonth = (month + 1) > 11 ? 1 : (month + 1);
        let startWeek = new Date(year + ',' + (month + 1) + ',' + 1).getDay();                          //目标月1号对应的星期
        let dayNums = new Date(year, nextMonth, 0).getDate();               //获取目标月有多少天
        let obj = {};
        let num = 0;
        if (month + 1 > 11) {
            nextYear = year + 1;
            dayNums = new Date(nextYear, nextMonth, 0).getDate();
        }
        arrLen = startWeek + dayNums;
        for (let i = 0; i < arrLen; i++) {
        if (i >= startWeek) {
            num = i - startWeek + 1;
            obj = {
                isToday: '' + year + (month + 1) + num,
                dateNum: num,
                weight: 5
            }
        } else {
            obj = {};
        }
            dateArr[i] = obj;
        }
        this.data.dateArr = dateArr;
        console.log(this.data.dateArr,'date==');
        let nowDate = new Date();
        let nowYear = nowDate.getFullYear();
        let nowMonth = nowDate.getMonth() + 1;
        let nowWeek = nowDate.getDay();
        let getYear = setYear || nowYear;
        let getMonth = setMonth >= 0 ? (setMonth + 1) : nowMonth;
        if (nowYear == getYear && nowMonth == getMonth) {
            this.data.isTodayWeek = true,
            this.data.todayIndex = nowWeek
        } else {
            this.data.isTodayWeek = false;
            this.data.todayIndex = -1
        }
    },
    /**
     * 上月切换
     */
    lastMonth() {
        //全部时间的月份都是按0~11基准，显示月份才+1
        let year = this.data.month - 2 < 0 ? this.data.year - 1 : this.data.year;
        let month = this.data.month - 2 < 0 ? 11 : this.data.month - 2;
        this.data.year = year,
        this.data.month = month + 1
        this.dateInit(year, month);
    },
    /**
     * 下月切换
     */
    nextMonth() {
        //全部时间的月份都是按0~11基准，显示月份才+1
        let year = this.data.month > 11 ? this.data.year + 1 : this.data.year;
        let month = this.data.month > 11 ? 0 : this.data.month;
        this.data.year = year;
        this.data.month = (month + 1);
        this.dateInit(year, month);
    }
  }
}

</script>
<style lang='scss' scoped>
.calendarBox{
  border: .5px solid #eee;
}
.calendar_title {
  display: flex;
  height: 30px;
  align-items: center;
  font-size: 12px;
  justify-content: center;
  background: #eee;
  color: #666;
  a{
      display: inline-block;
      width: 100px;
      text-align: center;
  }
  i{
      text-align: center;
      display: inline-block;
  }
}

/* 日历 */
.calendar {
  width: 100%;
  background: #fff;
  border-bottom-right-radius: 20rpx;
  border-bottom-left-radius: 20rpx;
  font-family: FZZhunYuan-M02S;
}
.header {
  font-size: 0;
  margin: 0 auto;
}
.header > div {
  display: inline-block;
  width: 14.285%;
  color: #666;
  font-size: 10px;
  text-align: center;
  padding: 5px 0;
}
.weekMark {
  position: relative;
  margin: 0 auto;
}
.weekMark div {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  border-bottom: 2px solid #69f;
}
.date-box {
  font-size: 0;
  padding: 5px 0;
  margin: 0 auto;
}
.date-box > div {
  position: relative;
  display: inline-block;
  width: 14.285%;
  color: #666;
  text-align: center;
  vertical-align: middle;
}
.date-head {
  height: 60rpx;
  line-height: 60rpx;
  font-size: 10px;
}
.nowDay .date-head {
  width: 15px;
  height: 15px;
  line-height: 15px;
  border-radius: 50%;
  text-align: center;
  color: #fff;
  background-color: #ff9933;
  margin: 0 auto;
}
</style>