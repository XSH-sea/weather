<template>
  <div id="search">
    <div class="header">
      <i class="back iconfont icon-icon_left" @click="back()"></i>
      <p class="title">添加城市</p>
    </div>
    <div class="searchBox">
      <input type="search" name id v-model="keyWord" @focus="clear()"  @keyup.enter="search()"/>
      <i class="iconfont icon-icon_search" @click="search()" ></i>
    </div>
    <div class="list" v-show="searchFlag">
      <ul>
        <li
          v-for="(val,index) in cityList"
          :key="index"
          @click="addHistory(val.location)"
        >{{val.location}}-{{val.parent_city}}-{{val.admin_area}}</li>
      </ul>
    </div>
    <div class="history" v-show="historyFlag">
      <div class="title">
        <h3>搜索历史</h3>
        <i class="iconfont icon-icon_delete" @click="delHistory"></i>
      </div>
      <ul>
        <li v-for="(val,index) in history" :key="index" @click="refreshto(val)">{{val}}</li>
      </ul>
    </div>
    <div class="hotCity">
      <h3>热门城市</h3>
      <ul>
        <li v-for="(val,index) in hotCity" :key="index" @click="refreshto(val)">{{val}}</li>
      </ul>
    </div>
    <err class="err" v-if="errFlag"></err>
  </div>
</template>

<script>
import err from "@/components/err";
export default {
  data() {
    return {
      hotCity: [],
      cityList: [],
      history: [],
      errFlag: false,
      searchFlag: false,
      historyFlag: true,
      keyWord: "请输入需要搜索的城市名称"
    };
  },
  created() {
    this.isHave();
    this.getHotCity();
  },
  methods: {
    //返回上一页
    back() {
      this.$router.back(-1);
    },
    //获取热门城市
    getHotCity() {
      this.axios
        .get(
          "https://search.heweather.net/top?group=cn&key=415c7d28177f4749b004841b3f77b59c"
        )
        .then(res => {
          this.errFlag = false;
          let result = res.data.HeWeather6[0].basic;
          for (let i = 0; i < result.length; i++) {
            this.hotCity.push(result[i].location);
          }
        })
        .catch(err => {
          console.log(err);
          this.errFlag = true;
        });
    },
    //搜索功能
    clear() {
      this.keyWord = "";
      this.searchFlag = false;
    },
    //搜索
    search() {
      if (this.keyWord != "" && this.keyWord != "请输入需要搜索的城市名称") {
        this.axios
          .get(
            "https://search.heweather.net/find?key=415c7d28177f4749b004841b3f77b59c&group=cn&number=10&location=" +
              this.keyWord
          )
          .then(res => {
            console.log(res);
            //判断是否由此城市
            if (res.data.HeWeather6[0].status == "ok") {
              this.searchFlag = true;
              this.cityList = res.data.HeWeather6[0].basic;
            } else if (res.data.HeWeather6[0].status == "unknown location") {
              this.keyWord = "抱歉，该城市不存在，请重新查询。";
            }
          })
          .catch(err => {
            console.log(err);
          });
      } else {
        this.searchFlag == false;
      }
    },
    //历史搜索的添加并跳转
    addHistory(val) {
      var historyArr = [];
      //获取原来历史
      historyArr = JSON.parse(localStorage.getItem("history"));
      console.log(JSON.parse(localStorage.getItem("history")));
      //判断该历史是否存在
      if (historyArr.indexOf(val) > -1) {
        // 存在
        this.$store.state.cityName = val;
        this.$router.push("/");
      } else {
        //不存在
        //添加
        historyArr.push(val);
        //存储
        localStorage.setItem("history", JSON.stringify(historyArr));
        //挂载到页面
        this.historyFlag = true;
        this.history = historyArr;
        console.log(JSON.parse(localStorage.getItem("history")));
        this.$store.state.cityName = val;
        this.$router.push("/");
      }
    },
    //删除搜索记录
    delHistory() {
      localStorage.removeItem("history");
      this.historyFlag = false;
    },
    //判断是否存在搜索历史
    isHave() {
      if (
        JSON.parse(localStorage.getItem("history")) == null ||
        JSON.parse(localStorage.getItem("history")).length == 0
      ) {
        //不存在
        var historyArr = [];
        localStorage.setItem("history", JSON.stringify(historyArr));
        this.historyFlag = false;
      } else {
        //存在
        this.historyFlag = true;
        this.history = JSON.parse(localStorage.getItem("history"));
      }
    },
    refreshto(val) {
      this.$store.state.cityName = val;
      this.$router.push("/");
    }
  },
  components: {
    err
  }
};
</script>

<style scoped>
.err {
  position: absolute;
  top: 240px;
  left: 50%;
  margin-left: -110px;
}

#search {
  position: relative;
}

.header {
  width: 100%;
  height: 40px;
   background-color: rgb(225, 233, 220);
  position: relative;
}

.header .back {
  position: absolute;
  top: 0;
  left: 5px;
  height: 40px;
  font-size: 20px;
  line-height: 40px;
}

.header .title {
  height: 40px;
  font-size: 20px;
  line-height: 40px;
}

.searchBox {
  width: 100%;
  height: 24px;
  margin-top: 5px;
}

.searchBox input {
  background-color: rgba(167,220,224,.5);
  width: 86%;
  height: 24px;
  float: left;
  border: 1px solid rgba(28,120,135,.4);
  border-radius: 12px;
  margin-left: 5px;
  padding: 0 12px;
  opacity: 0.9;
}

.searchBox input:focus {
  outline: none;
}

.searchBox i {
  height: 22px;
  width: 10%;
  border: 1px solid rgba(28,120,135,.4);
  background-color: rgba(167,220,224,.3);
  float: right;
  margin-right: 5px;
  line-height: 22px;
  font-size: 18px;
  border-radius: 12px;
}
  
.list {
  width: 98%;
  margin: 0 auto;
  /* background-color: #ffe; */
  border-radius: 8px;
  border: 1px solid #eee;
}

.list ul {
  list-style: none;
  background-color: rgba(225, 233, 220,.1)
}

.list ul li {
  text-align: left;
  padding-left: 6px;
  margin: 0 10px;
  border-bottom: 1px solid #eee;
  font-size: 14px;
}

.list ul li:last-child {
  border: none;
}

.hotCity {
  width: 100%;
  clear: both;
  margin-top: 15px;
}

.hotCity h3 {
  text-align: left;
  margin-left: 10px;
}

.hotCity ul {
  width: 90%;
  margin: 5px auto 0;
  list-style: none;
}

.hotCity ul li {
  float: left;
  margin: 0 8px 8px 0;
  padding: 0 8px;
  border-radius: 12px;
  background-color: rgba(214, 200, 75,.2);
}

.history {
  width: 100%;
  margin: 15px 0;
}

.history .title {
  width: 100%;
  height: 20px;
}

.history h3 {
  float: left;
  margin-left: 10px;
}

.history i {
  height: 18px;
  width: 18px;
  float: right;
  margin-right: 10px;
}

.history ul {
  width: 90%;
  margin: 5px auto 0;
  list-style: none;
}

.history ul li {
  float: left;
  margin: 0 8px 8px 0;
  padding: 0 8px;
  border-radius: 12px;
  background-color: #eee;
}
</style>