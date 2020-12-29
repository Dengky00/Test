<template>
  <div class="container">
<!--    <div class="swiper-bg"-->
<!--         :style="{backgroundColor:slidesColor[index]}">-->
<!--    </div>-->
    <div class="header_container">
    <div class="header_img"><img src="../assets/images/logo-round.png"/></div>
		<div class="header_search">
				<div>
					<input type="text" placeholder="搜索  商品名称" v-model="keywords"/>
          <button type="button" class="btn btn-default btn-sm">
          <span class="glyphicon glyphicon-search"></span></button>
				</div>
				<p>
					<a>自营日满减</a>
					<a>西二女装</a>
					<a>笔记本电脑</a>
					<a>电子书</a>
					<a>限时秒杀</a>
				</p>
		</div>
		<div class="shopping_bag">
      <span class="glyphicon glyphicon-shopping-cart"></span>
      <router-link to='/cart'>我的购物车</router-link>
		</div>
	  </div>
    <div class="stage">
      <ul class="category-nav">
        <li
          v-for="(item, index) in navbars"
          :key="index"
          class="cate-nav-item">
          <i class="cate-nav-icon" :class="item.icon"></i>
          {{item.text}}
        </li>
      </ul>
      <div class="swiper">
        <Swiper :slides="slidesImage" v-model="index"></Swiper>
      </div>
    </div>
    <div class="rec-banner">
      <h1 class="banner-title">精品推荐</h1>
      <ul class="rec-list">
        <li
          class="rec-card"
          v-for="(item,index) in goods"
          :key="index"
          @click="togglePage(item)">
          <img :src="item.cover" class="rec-media" />
          <div class="rec-profile">
            <h4>{{item.text}}</h4>
            <p class="rec-params">
              原价：<span class="rec-price">¥{{item.price}}</span>
              促销价：<span class="rec-online-price">¥{{item.onlinePrice}}</span>
            </p>
          </div>
        </li>
      </ul>
    </div>
    <router-link to='/order'><button class="ui basic blue button">订单</button></router-link>
    <router-link to='/login'><button class="ui basic blue button">登录</button></router-link>
  </div>
</template>

<script>
  import Swiper from '@/widgets/Swiper'
  import config from '@/config/config'
  export default {
    name: "Index",
    components: {Swiper},
    data() {
      return{
        index:0
      }
    },
    computed: {
      navbars () {
        return config.navbars
      },
      goods () {
        return config.goods
      },
      // slidesColor () {
      //   return config.goods.map(item => item.color)
      // },
      slidesImage () {
        return config.goods.map(item => item.poster)
      }
    },
    methods: {
      togglePage (item) {
        this.$router.push({path: 'goods', query: { name: item.name}})
      }
    }
  }
</script>

<style scoped>

  .container {
    position: relative;
    background-color: #f5f5f5;
    border-bottom: 1px solid transparent;
  }
  .swiper-bg {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 500px;
    background-color: #e5e5e5;
  }
  .stage {
    width: 1120px;
    margin-left: auto;
    margin-right: auto;
    background-color: #789;
  }
  .category-nav {
    /*display: inline-block;*/
    position: absolute;
    width: 200px;
    height: 500px;
    z-index: 2;
    list-style: none;
    background-color: rgba(0, 0, 0, 0.55);
    margin-top: 0px;
  }
  .cate-nav-item {
    padding-left: 12px;
    line-height: 35.7143px;
    color: #fff;
    cursor: pointer;
  }
  .cate-nav-item:hover {
    color: #787878;
    background-color: rgba(255, 255, 255, .8);
  }
  .cate-nav-icon {
    opacity: .5;
  }
  .swiper {
    height: 500px;
    background-color: #e8e8e8;
  }
  .rec-banner {
    margin: 30px auto;
    padding-top: 30px;
    padding-bottom: 50px;
    width: 1120px;
    background-color: #fff;
  }
  .banner-title {
    padding: 8px 15px;
  }
  .rec-list {
    list-style: none;
  }
  .rec-card {
    display: inline-block;
    width: 25%;
    text-align: center;
    vertical-align: top;
    cursor: pointer;
  }
  .rec-media {
    width: 240px;
  }
  .rec-profile {
    width: 200px;
    display: inline-block;
    color: #444;
  }
  .rec-price {
    text-decoration: line-through;
  }
  .rec-online-price {
    color: #ff0036;
    font-size: 16px;
  }
  .rec-params {
    font-size: 12px;
    color: #888;
  }
/*头部搜索区*/
.header_container{
	position: relative;
	width: 100%;
  height: 140px;
  margin: 0;
  padding: 0;
}
/*商城标识图片区域*/
.header_container>.header_img{
	position: absolute;
	left: 100px;
	margin-top: 10px;
	width: 100px;
	height: 100px;
  border: 1px solid darkgray;
  box-shadow: 2px 4px 15px rgba(45,45,45,0.15);
  border-radius: 50%;
}
.header_img>img{
	width: 100%;
	height: 100%;
	border-radius: 50%;
}
/*鼠标移入图片实现3d动画*/
.header_img:hover{
	transform-style: preserve-3d;
	transform:rotateY(360deg);
    transition: all 1500ms;
    -moz-transform-style: preserve-3d;
	-moz-transform:rotateY(45deg);
	-moz-transition: all 1500ms;
}
.header_search{
	position: absolute;
	left: 50%;
	margin-left: -290px;
	margin-top: 50px;
}
.header_search div{
  display: flex;
  align-items: center;
}
.header_search input{
	padding-left: 10px;
	width: 490px;
	height: 35px;
	font-size: 14px;
	line-height: 35px;
	border: 2px solid #FF0236;
	outline: none;
}
.header_search button.el-button.el-button--danger{
  padding: 0;
  width: 60px;
  height: 35px;
	font-size: 18px;
  border-radius: 0;
  outline: none;

  display: flex;
  justify-content: center;
  align-items: center;
}
.header_search>p>a{
	display: inline-block;
	padding: 5px 10px;
	font-size: 12px;
	color: #999;
	cursor: pointer;
}
.header_search>p>a:hover{
	color: red;
}
/*头部的购物车标记区域*/
.header_container>.shopping_bag{
	position: absolute;
	margin-top: 60px;
	right: 120px;
	width: 190px;
	height: 35px;
	text-align: center;
	line-height: 35px;
	font-size: 12px;
	background: #f8f9fa;
	color: red;
	cursor: pointer;
}
.shopping_bag>img{
	display: inline-block;
	margin-left: 5px;
	margin-top: 5px;
	width: 17px;
	height: 17px;
}
.shopping_bag>a{
	color: red;
}
</style>
