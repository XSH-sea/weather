<template>
  <div id="index">
    <div class="header">
      <i class="iconfont icon-icon_add" @click="goSearch()"></i>
      <p class="cityName">{{cityName}}</p>
    </div>
    <div class="cond">
      <p class="nowCond">{{nowCond}}</p>
      <p class="nowTmp">{{nowTmp}}</p>
      <p class="aqi">{{aqi}}</p>
    </div>
    <div class="lifeStyle">
      <div class="border">
        <ul ref="ulEle" :style="{top:Top+'px'}">
          <li v-for="(val,index) in lifeStyle" :key="index">
            <p class="title">{{lifeStyle[index].title}}</p>
            <p class="text">{{lifeStyle[index].text}}</p>
          </li>
          <li>
            <p class="title">{{lifeStyle[0].title}}</p>
            <p class="text">{{lifeStyle[0].text}}</p>
          </li>
        </ul>
      </div>
    </div>
    <div class="hourly" ref="border">
      <div
        class="hourlyArea"
        ref="hourly"
        @touchstart="start($event)"
        @touchmove="move($event)"
        @touchend="end($event)"
        :style="{left:hourlyLeft+'px'}"
      ></div>
      <!-- <div class="hourlyArea" ref="hourly" @touchstart="start($event)" @touchmove="move($event)" @touchend="end($event)" :style="touchFlag==2?{left:hourlyLeft+'px'}:touchStyle[touchFlag]"></div> -->
    </div>
    <div class="daily">
      <ul>
        <li class="daily0">
          <div class="time">
            <span class="date">{{daily0.date}}</span>
            <span class="week">{{daily0.week}}</span>
          </div>
          <div class="info">
            <span class="day">
              <img class="icon_d" :src="daily0.icon_url_d" />
              <p>{{daily0.cond_txt_d}}</p>
            </span>
            <span class="night">
              <img class="icon_n" :src="daily0.icon_url_n" />
              <p>{{daily0.cond_txt_n}}</p>
            </span>
          </div>
          <div class="tmp">{{daily0.tmp}}</div>
          <div class="sun">
            <span class="up">日出:{{daily0.sr}}</span>
            <span class="down">日落:{{daily0.ss}}</span>
          </div>
        </li>
        <li
          v-for="(val,index) in daily1"
          :key="index"
          class="daily1"
          :class="(index+1)%2==0?'right':'left'"
        >
          <div class="time">
            <span class="date">{{val.date}}</span>
            <span class="week">{{val.week}}</span>
          </div>
          <div class="info">
            <span class="day">
              <img class="icon_d" :src="val.icon_url_d" />
              <p>{{val.cond_txt_d}}</p>
            </span>
            <span class="night">
              <img class="icon_n" :src="val.icon_url_n" />
              <p>{{val.cond_txt_n}}</p>
            </span>
          </div>
          <div class="tmp">{{val.tmp}}</div>
          <div class="sun">
            <span class="up">日出:{{val.sr}}</span>
            <span class="down">日落:{{val.ss}}</span>
          </div>
        </li>
      </ul>
    </div>
    <err class="err" v-if="errFlag"></err>
  </div>
</template>

<script>
import err from "@/components/err";
export default {
  name: "index",
  data() {
    return {
      errFlag: false,
      Top: 0,
      touch0: 0,
      touch1: 0,
      hourlyLeft: 0,
      key: "415c7d28177f4749b004841b3f77b59c",
      cityName: "",
      nowCond: "晴",
      nowTmp: "0℃",
      aqi: "无法获取",
      lifeStyle: [
        { title: "穿衣指南", text: "无法获取" },
        { title: "旅游指南", text: "无法获取" },
        { title: "出行指南", text: "无法获取" },
        { title: "防晒指南", text: "无法获取" }
      ],
      daily: [
        {
          date: "12.01",
          week: "星期一",
          tmp: "4~5℃",
          icon_url_d: "../../static/weather-icon/100.png",
          icon_url_n: "../../static/weather-icon/100n.png",
          cond_txt_d: "晴",
          cond_txt_n: "多云",
          sr: "07:36",
          ss: "19:23"
        },
        {
          date: "12.01",
          week: "星期一",
          tmp: "4~5℃",
          icon_url_d: "../../static/weather-icon/100.png",
          icon_url_n: "../../static/weather-icon/100n.png",
          cond_txt_d: "晴",
          cond_txt_n: "多云",
          sr: "07:36",
          ss: "19:23"
        },
        {
          date: "12.01",
          week: "星期一",
          tmp: "4~5℃",
          icon_url_d: "../../static/weather-icon/100.png",
          icon_url_n: "../../static/weather-icon/100n.png",
          cond_txt_d: "晴",
          cond_txt_n: "多云",
          sr: "07:36",
          ss: "19:23"
        },
        {
          date: "12.01",
          week: "星期一",
          tmp: "4~5℃",
          icon_url_d: "../../static/weather-icon/100.png",
          icon_url_n: "../../static/weather-icon/100n.png",
          cond_txt_d: "晴",
          cond_txt_n: "多云",
          sr: "07:36",
          ss: "19:23"
        },
        {
          date: "12.01",
          week: "星期一",
          tmp: "4~5℃",
          icon_url_d: "../../static/weather-icon/100.png",
          icon_url_n: "../../static/weather-icon/100n.png",
          cond_txt_d: "晴",
          cond_txt_n: "多云",
          sr: "07:36",
          ss: "19:23"
        },
        {
          date: "12.01",
          week: "星期一",
          tmp: "4~5℃",
          icon_url_d: "../../static/weather-icon/100.png",
          icon_url_n: "../../static/weather-icon/100n.png",
          cond_txt_d: "晴",
          cond_txt_n: "多云",
          sr: "07:36",
          ss: "19:23"
        },
        {
          date: "12.01",
          week: "星期一",
          tmp: "4~5℃",
          icon_url_d: "../../static/weather-icon/100.png",
          icon_url_n: "../../static/weather-icon/100n.png",
          cond_txt_d: "晴",
          cond_txt_n: "多云",
          sr: "07:36",
          ss: "19:23"
        }
      ],
      hourly: [
        {
          time: "00:00",
          tmp: "21"
        },
        {
          time: "01:00",
          tmp: "18"
        },
        {
          time: "02:00",
          tmp: "19"
        },
        {
          time: "03:00",
          tmp: "15"
        },
        {
          time: "04:00",
          tmp: "18"
        },
        {
          time: "05:00",
          tmp: "18"
        },
        {
          time: "06:00",
          tmp: "21"
        },
        {
          time: "07:00",
          tmp: "29"
        },
        {
          time: "08:00",
          tmp: "10"
        },
        {
          time: "09:00",
          tmp: "21"
        },
        {
          time: "10:00",
          tmp: "21"
        },
        {
          time: "11:00",
          tmp: "21"
        },
        {
          time: "12:00",
          tmp: "21"
        },
        {
          time: "13:00",
          tmp: "25"
        },
        {
          time: "14:00",
          tmp: "21"
        },
        {
          time: "15:00",
          tmp: "18"
        },
        {
          time: "16:00",
          tmp: "21"
        },
        {
          time: "17:00",
          tmp: "16"
        },
        {
          time: "18:00",
          tmp: "21"
        },
        {
          time: "19:00",
          tmp: "21"
        },
        {
          time: "20:00",
          tmp: "19"
        },
        {
          time: "21:00",
          tmp: "21"
        },
        {
          time: "22:00",
          tmp: "21"
        },
        {
          time: "23:00",
          tmp: "25"
        }
      ]
    };
  },
  created() {
    console.log(this.$store.state.cityName);
    this.cityName = this.$store.state.cityName;
    if (this.cityName === "") {
      this.getLocation();
    } else {
      this.getInfo();
    }
  },
  mounted() {
    this.scroll();
    console.log(this.daily, 1);
  },
  methods: {
    //轮播
    scroll() {
      console.log(this.$refs.ulEle.offsetHeight / 5 / 10);
      var scrollTimeId = setInterval(() => {
        var flag = 0;
        var timeId = setInterval(() => {
          this.Top -= this.$refs.ulEle.offsetHeight / 5 / 11;
          flag++;
          if (flag == 11) {
            clearInterval(timeId);
          }
          if (this.Top <= (-this.$refs.ulEle.offsetHeight / 5) * 4) {
            this.Top = 0;
          }
        }, 60);
        //页面跳转后销毁定时器
        this.$once("hook:beforeDestroy", () => {
          clearInterval(timeId);
        });
      }, 3000);
      this.$once("hook:beforeDestroy", () => {
        clearInterval(scrollTimeId);
      });
    },
    //温度折线绘制
    drawLine() {
      let timeArr = [];
      let tmpArr = [];
      let arr = [];

      for (let i = 0; i < this.hourly.length; i++) {
        timeArr.push(this.hourly[i].time);
        tmpArr.push(this.hourly[i].tmp);
      }

      tmpArr.forEach(e => arr.push(e));
      arr.sort(function(a, b) {
        return a - b;
      });

      let lineChart = this.$echarts.init(this.$refs.hourly);

      lineChart.setOption({
        xAxis: {
          data: timeArr,
          axisLine: {
            show: false
          },
          axisTick: {
            show: false
          },
          axisLabel: {
            color: "rgba(28,120,135,0.8)"
          }
        },
        yAxis: {
          show: false,
          max: arr[arr.length - 1],
          min: arr[0]
        },
        grid: {
          top: 24,
          bottom: 30,
          left: 0,
          right: 0
        },
        series: [
          {
            type: "line",
            data: tmpArr,
            label: {
              show: true,
              color: "rgba(38,188,213,0.8)"
            },
            lineStyle: {
              color: "rgba(28,120,135,0.8)"
            },
            itemStyle: {
              color: "rgba(38,188,213,0.8)"
            },
            hoverAnimation: false
          }
        ]
      });
    },
    //温度曲线滑动
    start(e) {
      this.touch0 = Math.floor(e.touches[0].clientX);
    },
    move(e) {
      this.touch1 = Math.floor(e.touches[0].clientX);
      var left = Math.floor(this.$refs.hourly.offsetLeft);
      var width = Math.floor(this.$refs.hourly.offsetWidth);
      var borderWidth = Math.floor(this.$refs.border.offsetWidth);
      var temp = this.touch0 - this.touch1;
      if (left <= borderWidth - width && temp > 0) {
        this.hourlyLeft = borderWidth - width;
        // console.log(1,this.hourlyLeft)
      } else if (left >= 0 && temp < 0) {
        this.hourlyLeft = 0;
        // console.log(2,this.hourlyLeft)
      } else {
        this.hourlyLeft = left - temp;
      }
    },
    end(e) {
      this.touch0 = 0;
      this.touch1 = 0;
    },
    goSearch() {
      this.$router.push("/search");
    },
    //获取当前位置
    getLocation() {
      //高德定位
      AMap.plugin("AMap.CitySearch", () => {
        var citySearch = new AMap.CitySearch();
        citySearch.getLocalCity((status, result) => {
          if (status === "complete" && result.info === "OK") {
            //定位成功
            this.cityName = result.city;
            this.getInfo();
          } else {
            //定位失败，跳转到搜索页面
            this.cityName = "请手动选择城市";
            alert("抱歉，无法定位当前城市，请手动选择城市！");
            this.goSearch();
          }
        });
      });
    },
    //获取天气信息
    getInfo() {
      var api = "https://api.heweather.net/s6/weather/";
      //获取实时天气
      this.axios
        .get(api + "now", {
          params: {
            key: this.key,
            location: this.cityName
          }
        })
        .then(res => {
          this.nowCond = res.data.HeWeather6[0].now.cond_txt;
          this.nowTmp = res.data.HeWeather6[0].now.tmp + "℃";
        })
        .catch(err => {
          console.log(err);
          this.errFlag = true;
        });

      //获取空气质量
      this.axios
        .get("https://api.heweather.net/s6/air/now", {
          params: {
            key: this.key,
            location: this.cityName
          }
        })
        .then(res => {
          var aqi = res.data.HeWeather6[0].air_now_city.aqi;
          var qlty = res.data.HeWeather6[0].air_now_city.qlty;
          var txt = "空气指数";
          this.aqi = txt + aqi + " " + qlty;
        })
        .catch(err => {
          console.log(err);
          this.errFlag = true;
        });

      //获取生活指南
      this.axios
        .get(api + "lifestyle", {
          params: {
            key: this.key,
            location: this.cityName
          }
        })
        .then(res => {
          var LS = this.lifeStyle;
          var result = res.data.HeWeather6[0].lifestyle;
          LS[0].text = result[1].txt;
          LS[1].text = result[4].txt;
          LS[2].text = result[13].txt;
          LS[3].text = result[12].txt;
        })
        .catch(err => {
          console.log(err);
          this.errFlag = true;
        });

      //获取每小时温度
      this.axios
        .get(api + "hourly", {
          params: {
            key: this.key,
            location: this.cityName
          }
        })
        .then(res => {
          var result = res.data.HeWeather6[0].hourly;
          for (var i = 0; i < 24; i++) {
            this.hourly[i].tmp = result[i].tmp;
            this.hourly[i].time = result[i].time.substring(11, 16);
          }
          this.drawLine();
        })
        .catch(err => {
          console.log(err);
          this.errFlag = true;
        });

      // 获取七天天气预报
      this.axios
        .get(api + "forecast", {
          params: {
            key: this.key,
            location: this.cityName
          }
        })
        .then(res => {
          console.log(res);
          var result = res.data.HeWeather6[0].daily_forecast;
          var daily = this.daily;
          // 计算日期
          var d = new Date();
          var day = d.getDay();
          var weeks = [
            "星期日",
            "星期一",
            "星期二",
            "星期三",
            "星期四",
            "星期五",
            "星期六"
          ];
          for (var i = 0; i < 7; i++) {
            if (day < 7) {
              daily[i].week = weeks[day];
              day++;
            } else {
              daily[i].week = weeks[day - 7];
              day++;
            }
            daily[i].date = result[i].date.substring(5, 10).replace("-", ".");
            daily[i].tmp = result[i].tmp_min + "~" + result[i].tmp_max + "℃";
            daily[i].cond_txt_d = result[i].cond_txt_d;
            daily[i].cond_txt_n = result[i].cond_txt_n;
            daily[i].icon_url_d =
              "./static/img/" + result[i].cond_code_d + ".png";
            //晚上天气图标有些会有不同
            if (
              result[i].cond_code_n == 100 ||
              result[i].cond_code_n == 103 ||
              result[i].cond_code_n == 104 ||
              result[i].cond_code_n == 300 ||
              result[i].cond_code_n == 301 ||
              result[i].cond_code_n == 406 ||
              result[i].cond_code_n == 407
            ) {
              result[i].cond_code_n = result[i].cond_code_n + "n";
            }
            daily[i].icon_url_n =
              "./static/img/" + result[i].cond_code_n + ".png";

            daily[i].ss = result[i].ss;
            daily[i].sr = result[i].sr;
          }
        })
        .catch(err => {
          console.log(err);
          this.errFlag = true;
        });
    }
  },
  computed: {
    daily0: function() {
      return this.daily[0];
    },
    daily1: function() {
      var arr = [];
      for (var i = 1; i < 7; i++) {
        arr.push(this.daily[i]);
      }
      return arr;
    }
  },
  components: {
    err
  }
};
</script>

<style scoped>
@import "../assets/css/font.css";
#index {
  position: relative;
}

.err {
  position: absolute;
  top: 240px;
  left: 50%;
  margin-left: -110px;
}

.header {
  width: 100%;
  height: 40px;
  position: fixed;
  top: 0;
  border-bottom: 1px solid #eee;
  background-color: rgb(225, 233, 220);
}
.header .cityName {
  display: inline-block;
  height: 40px;
  font-size: 24px;
  font-weight: bold;
  line-height: 40px;
}

.header i {
  position: absolute;
  top: 0;
  left: 5px;
  height: 40px;
  font-size: 20px;
  font-weight: 700;
  line-height: 40px;
}

.cond {
  width: 100%;
  height: 130px;
  padding: 5px 0 15px 0;
  margin-top: 40px;
  background-color: rgba(38, 188, 213, 0.8);
  color: rgb(255, 233, 220);
}

.cond .nowCond {
  font-size: 55px;
  font-weight: 500;
  font-family: "Libian";
}

.cond .nowTmp {
  font-size: 28px;
  font-family: "libian";
  margin-top: -10px;
}

.cond .aqi {
  height: 30px;
  font-size: 20px;
  font-family: "libian";
  line-height: 30px;
  border-radius: 8px;
  background-color: rgb(167, 220, 224);
  color: #666;
  display: inline-block;
  padding: 0 5px;
}

.lifeStyle {
  width: 100%;
  height: 110px;
  margin-top: 15px;
}

.lifeStyle .border {
  width: 95%;
  height: 110px;
  background-color: rgb(167, 220, 224);
  position: relative;
  border-radius: 15px;
  list-style: none;
  left: 2.5%;
  overflow: hidden;
}

.lifeStyle .border ul {
  width: 100%;
  height: 550px;
  position: absolute;
}

.lifeStyle .border .title {
  width: 95%;
  height: 30px;
  margin: 0 auto;
  font-size: 20px;
  line-height: 30px;
  color: rgb(28, 120, 135);
}

.lifeStyle .border .text {
  width: 95%;
  height: 80px;
  margin: 0 auto;
  font-size: 16px;
}

.hourly {
  width: 95%;
  height: 100px;
  margin: 15px auto 0;
  border-radius: 15px;
  overflow: hidden;
  background-color: rgba(225, 233, 220, 0.8);
  position: relative;
}

.hourlyArea {
  width: 280%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
}

.daily {
  width: 100%;
  margin-top: 15px;
}

.daily ul {
  width: 95%;
  margin: 0 auto;
  list-style: none;
}

.daily0 {
  width: 100%;
  height: 90px;
  background-color: rgba(38, 188, 213, 0.8);
  border-radius: 14px;
  position: relative;
  margin-bottom: 8px;
  color: rgb(255, 233, 220);
}

.daily0 .time {
  position: absolute;
  top: 0;
  left: 10px;
  text-align: left;
}

.daily0 .time span {
  display: block;
}

.daily0 .time .date {
  font-size: 24px;
  margin-bottom: -5px;
}

.daily0 .info {
  position: absolute;
  top: 0;
  right: 10px;
}

.daily0 .info span {
  display: block;
  height: 25px;
}

.daily0 .info img {
  width: 25px;
  height: 25px;
  float: right;
}

.daily0 .info p {
  float: right;
  font-size: 14px;
  line-height: 25px;
  margin-right: 4px;
}

.daily0 .sun {
  font-size: 14px;
}

.sun {
  position: absolute;
  width: 100%;
  bottom: 0;
  left: 0;
}

.sun .up {
  float: left;
  margin-left: 8px;
}

.sun .down {
  float: right;
  margin-right: 8px;
}

.daily0 .tmp {
  font-size: 35px;
  padding-top: 20px;
}

.daily1 {
  width: 49%;
  height: 75px;
  background-color: rgba(38, 188, 213, 0.8);
  border-radius: 14px;
  position: relative;
  margin-bottom: 8px;
  color: rgb(255, 233, 220);
}

.left {
  float: left;
}

.right {
  float: right;
}

.daily1 .time {
  position: absolute;
  top: 0;
  left: 10px;
  text-align: left;
}

.daily1 .time span {
  display: block;
}

.daily1 .time .date {
  font-size: 16px;
}

.daily1 .time .week {
  margin-top: -5px;
  font-size: 12px;
}

.daily1 .info {
  position: absolute;
  right: 10px;
  top: 0px;
}

.daily1 .info span {
  display: block;
  height: 20px;
}

.daily1 .info img {
  float: right;
  height: 20px;
  width: 20px;
  margin-right: -2px;
}

.daily1 .info p {
  float: right;
  font-size: 12px;
  line-height: 20px;
  margin-right: 2px;
}

.daily1 .sun {
  font-size: 12px;
}

.daily1 .tmp {
  position: absolute;
  top: 32px;
  left: 10px;
  font-size: 16px;
  text-align: left;
}
</style>
