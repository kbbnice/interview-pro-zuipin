<template>
  <div id="app">
    <div class="search">
      <input type="text" class="search-text">
      <button class="search-btn">查找</button>
    </div>
    <div class="headlist" id="headlist">
      <div class="all-title" @click="showAll" v-show="ifAllList">全部</div>
      <ul>
        <li @click="showFamous">知名茶城</li>
        <li
          v-for="(item,index) in cityVisited"
          :key="index"
          v-show="!ifAllList"
          @click="showCity(item)"
        >{{item}}</li>
      </ul>
      <div class="city-more" :class="ifAllList ? 'show-list' : ''" @click="showAllList">
        <span>↓</span>
      </div>
      <div class="all-cities" v-show="ifAllList">
        <ul>
          <li @click="showFamous">知名茶城</li>
          <li
            v-for="percity in allCities"
            :key="percity.key"
            @click="showCity(percity)"
          >{{ percity }}</li>
        </ul>
      </div>
    </div>

    <div
      class="city-items"
      v-for="item in cityList"
      :key="item.key"
      v-show="item.name === ifCity || ifSee || ifFamous"
      @click="ifAllList = false"
    >
      <ul>
        <!-- items -->

        <li
          v-for="shop in item.items"
          :key="shop.key"
          v-show="ifFamous ? shop.famous === true : true"
        >
          <div class="item-img">
            <img :src="shop.src" alt="">
          </div>
          <div class="city-details">
            <h5 class="city-title ellipsis">{{ shop.title }}</h5>
            <p class="city-address">{{ shop.address }}</p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  name: "App",
  data() {
    return {
      ifSee: false, //是否显示所有列表
      ifCity: "", //是否显示单独某个城市列表
      ifAllList: false, //是否显示所有城市名单：
      ifFamous: true, //是否显示热门城市列表
      cityVisited: ["福建", "广东", "山西", "吉林"],
      cityList: [
        {
          name: "福建",
          items: [
            {
              title: "福建茶叶批发市场福建高桥大市场",
              address: "福建茶叶批发市场福建高桥大市场",
              /**
               * 
               * //如果不用require 就访问不到这张图片，不知道为什么。╭(╯^╰)╮
               * 
               */
              src: require("./assets/1.jpg"),
              famous: true
            },
            {
              title: "福建茶叶批发市场福建高桥大市场2",
              address: "福建茶叶批发市场福建高桥大市场2",
              src: require("./assets/1.jpg"),
              famous: false
            },
            {
              title: "福建茶叶批发市场福建高桥大市场3",
              address: "福建茶叶批发市场福建高桥大市场3",
              src: require("./assets/1.jpg"),
              famous: false
            }
          ]
        },
        {
          name: "广东",
          items: [
            {
              title: "广东茶叶批发市场广东高桥大市场11",
              address: "广东茶叶批发市场广东高桥大市场11",
              src: require("./assets/1.jpg"),
              famous: false
            },
            {
              title: "广东茶叶批发市场广东高桥大市场22",
              address: "广东茶叶批发市场广东高桥大市场22",
              src: require("./assets/1.jpg"),
              famous: false
            },
            {
              title: "广东茶叶批发市场广东高桥大市场33",
              address: "广东茶叶批发市场广东高桥大市场33",
              src: require("./assets/1.jpg"),
              famous: false
            }
          ]
        },
        {
          name: "山西",
          items: [
            {
              title: "山西茶叶批发市场山西高桥大市场11",
              address: "山西茶叶批发市场山西高桥大市场11",
              src: require("./assets/1.jpg"),
              famous: false
            },
            {
              title: "山西茶叶批发市场山西高桥大市场22",
              address: "山西茶叶批发市场山西高桥大市场22",
              src: require("./assets/1.jpg"),
              famous: false
            },
            {
              title: "山西茶叶批发市场山西高桥大市场33",
              address: "山西茶叶批发市场山西高桥大市场33",
              src: require("./assets/1.jpg"),
              famous: false
            }
          ]
        },
        {
          name: "重庆",
          items: [
            {
              title: "重庆茶叶批发市场重庆高桥大市场11",
              address: "重庆茶叶批发市场重庆高桥大市场11",
              src: require("./assets/1.jpg"),
              famous: false
            },
            {
              title: "重庆茶叶批发市场重庆高桥大市场22",
              address: "重庆茶叶批发市场重庆高桥大市场22",
              src: require("./assets/1.jpg"),
              famous: false
            },
            {
              title: "重庆茶叶批发市场重庆高桥大市场33",
              address: "重庆茶叶批发市场重庆高桥大市场33",
              src: require("./assets/1.jpg"),
              famous: false
            }
          ]
        },
        {
          name: "湖南",
          items: [
            {
              title: "湖南茶叶批发市场广东高桥大市场11",
              address: "湖南茶叶批发市场广东高桥大市场11",
              src: require("./assets/1.jpg"),
              famous: false
            },
            {
              title: "湖南茶叶批发市场广东高桥大市场22",
              address: "湖南茶叶批发市场广东高桥大市场22",
              src: require("./assets/1.jpg"),
              famous: false
            },
            {
              title: "湖南茶叶批发市场广东高桥大市场33",
              address: "广东茶叶批发市场广东高桥大市场33",
              src: require("./assets/1.jpg"),
              famous: false
            }
          ]
        },
        {
          name: "吉林",
          items: [
            {
              title: "吉林茶叶批发市场广东高桥大市场11",
              address: "吉林茶叶批发市场广东高桥大市场11",
              src: require("./assets/1.jpg"),
              famous: true
            },
            {
              title: "吉林茶叶批发市场广东高桥大市场22",
              address: "吉林茶叶批发市场广东高桥大市场22",
              src: require("./assets/1.jpg"),
              famous: false
            },
            {
              title: "吉林茶叶批发市场广东高桥大市场33",
              address: "吉林茶叶批发市场广东高桥大市场33",
              src: require("./assets/1.jpg"),
              famous: true
            }
          ]
        },
        {
          name: "湖北",
          items: [
            {
              title: "湖北茶叶批发市场广东高桥大市场11",
              address: "湖北茶叶批发市场广东高桥大市场11",
              src: require("./assets/1.jpg"),
              famous: true
            },
            {
              title: "湖北茶叶批发市场广东高桥大市场22",
              address: "湖北茶叶批发市场广东高桥大市场22",
              src: require("./assets/1.jpg"),
              famous: true
            },
            {
              title: "湖北茶叶批发市场广东高桥大市场33",
              address: "湖北茶叶批发市场广东高桥大市场33",
              src: require("./assets/1.jpg"),
              famous: false
            }
          ]
        }
      ],
      allCities: ["福建", "广东", "山西", "吉林", "重庆", "湖南", "湖北"]
    };
  },
  methods: {
    showAll() {
      this.ifSee = true;
      this.ifCity = "";
      this.ifAllList = false;
      this.ifFamous = false;
    },
    //显示城市列表：
    showCity(city) {
      this.ifSee = false;
      this.ifCity = city;
      this.ifFamous = false;
      this.cityVisited.unshift(city);

      for (var i = 0; i < this.cityVisited.length; i++) {
        if (this.cityVisited[0] == this.cityVisited[i] && i !== 0) {
          var aaa = this.cityVisited.splice(i, 1);
        }
      }
      this.cityVisited.length = 4;
      // this.cityVisited.pop(aaa);
      this.allCities.unshift(city);

      for (var i = 0; i < this.allCities.length; i++) {
        if (this.allCities[0] == this.allCities[i] && i !== 0) {
          var aaa = this.allCities.splice(i, 1);
        }
      }

      this.ifAllList = false;
    },
    //显示全部城市名单：
    showAllList() {
      this.ifAllList = this.ifAllList ? false : true;
    },
    //显示热门：
    showFamous() {
      this.ifFamous = true;
      this.ifAllList = false;
    }
  }
}

/**
 * 
 * 
 * 
 *       ****                ****
 *      *  *  *             *  *  *
 *      *  *  *             *  *  *
 *       ****                ****
 * 
 * 
 *                 *
 *                *
 *                * * * 
 * 
 *         *                 *
 *           *             * 
 *             * * * * * *
 * 
 * 
 * 终于写完了~~~~~~~~~~~~~~~~~~~~~~~~~~妈耶~~~~~~~~~~~~~开心
 * 
 * 睡觉~~~~~~~~~~~~~~~zzzzzzZZZZZZZZZ
 * 
 * 2019.04.20    凌晨：3:00
 * 
 * 人生第一段vue-cli 代码
 * 
 * 欧耶~
 * 
 * 晚安~柯宝~你是最棒（pang)的~~~~
 * 
 * 
 */
</script>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-size: 12px;
}
li {
  list-style: none;
}
#app {
  width: 100%;
  min-width: 300px;
}

/* 搜索 */

.search {
  width: 100%;
  text-align: center;
}
.search .search-text {
  width: 60%;
  height: 30px;
  margin: 10px 0;
  border: 1px solid grey;
}
.search .search-btn {
  border: none;
}

/* 城市选择 */
.headlist {
  position: relative;
  height: 40px;
  background-color: #f5f5f5;
  z-index: 1000;
}
.headlist ul {
  display: inline-block;
  width: 90%;
}
.headlist > ul > li {
  float: left;
  width: 20%;
  height: 40px;
  line-height: 40px;
  text-align: center;
  background-color: #f5f5f5;
}
.headlist .city-more {
  display: inline-block;
  position: absolute;
  right: 0;
  width: 10%;
  height: 40px;
  text-align: center;
  line-height: 40px;
  transition: 0.5s;
  -moz-transition: 0.5s; /* Firefox 4 */
  -webkit-transition: 0.5s; /* Safari 和 Chrome */
  -o-transition: 0.5s; /* Opera */
  transform: rotate(0deg);
  -ms-transform: rotate(0deg); /* IE 9 */
  -moz-transform: rotate(0deg); /* Firefox */
  -webkit-transform: rotate(0deg); /* Safari 和 Chrome */
  -o-transform: rotate(0deg); /* Opera */
}
.headlist .city-more.show-list {
  transition: 0.5s;
  -moz-transition: 0.5s; /* Firefox 4 */
  -webkit-transition: 0.5s; /* Safari 和 Chrome */
  -o-transition: 0.5s; /* Opera */
  transform: rotate(180deg);
  -ms-transform: rotate(180deg); /* IE 9 */
  -moz-transform: rotate(180deg); /* Firefox */
  -webkit-transform: rotate(180deg); /* Safari 和 Chrome */
  -o-transform: rotate(180deg); /* Opera */
}

/* 弹出所有城市 */
.all-cities {
  position: absolute;
  top: 40px;
  width: 100%;
  background-color: white;
}
.all-title {
  position: absolute;
  width: 20%;
  height: 40px;
  text-align: center;
  line-height: 40px;
  background-color: #f5f5f5;
  z-index: 4;
}
.all-cities > ul {
  width: 100%;
  overflow: hidden;
}
.all-cities > ul > li {
  float: left;
  width: 18%;
  height: 35px;
  margin: 10px 1%;
  line-height: 35px;
  text-align: center;
  background-color: rgb(255, 244, 220);
}

/* 是否选中 */
.hot-focus {
  /* background-color: rgb(255, 239, 187); */
  color: rgb(253, 173, 0);
}
.hot-blur {
  background-color: white;
}

/* 城市详情 */

.city-items {
  background-color: #f5f5f5;
}
.city-items > ul > li {
  margin: 2px;
  background-color: #fff;
}
.item-img {
  position: relative;
  display: inline-block;
  width: 80px;
  height: 80px;
  z-index: 10;
}
.item-img img {
  max-width: 100%;
  height: auto;
  max-height: 100%;
}
.city-details {
  display: inline-block;
  vertical-align: top;
  width: 100%;
  height: 80px;
  padding-left: 90px;
  margin-left: -85px;
}
.city-details .city-title {
  margin: 1px 1px 4px;
  font-size: 13px;
}
.city-details .city-address {
  height: 40px;
  margin: 4px;
  font-size: 11px;
  line-height: 11px;
}
.focus {
  color: rgb(255, 81, 0);
}
/* 共有属性 */
.ellipsis {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
</style>
