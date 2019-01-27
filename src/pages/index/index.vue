<template>
  <!-- 顶部结构 -->
  <div class="index-container">
    <div class="search-box">
      <input type="text" placeholder="搜索">
      <icon type="search" size="12"></icon>
    </div>
    <!-- 轮播图 -->
    <div class="swiper-container">
      <swiper indicator-dots autoplay circular indicator-active-color="#0094ff">
        <swiper-item v-for="item in swiperList" :key="item.image_src">
          <img mode="aspectFill" :src="item.image_src">
        </swiper-item>
      </swiper>
    </div>
    <!-- 分类区域 -->
    <div class="category-container">
      <div class="item" v-for="item in categoryList">
        <img :src="item.image_src" alt>
        <p>{{item.name}}</p>
      </div>
    </div>
  </div>
</template>

<script>
//引入hxios模块
import hxios from "../../utils/index.js";
export default {
  data() {
    return {
      //轮播图数组
      swiperList: [],
      //分类的数据
      categoryList: []
    };
  },
  //初始化的时候 获取数据
  async created() {
    //   轮播图数据
    let swiperRes = await hxios.get({
      url: "api/public/v1/home/swiperdata"
    });
    this.swiperList = swiperRes.data.message;
    //分类接口数据
    let cateGoryRes = await hxios.get({
      url: "api/public/v1/home/catitems"
    });
    this.categoryList = cateGoryRes.data.message;
  }
};
</script>

<style lang="scss">
$uRed: #ff2d4a;
// 顶部的样式
.index-container {
  padding-top: 100rpx;
}
.search-box {
  background-color: $uRed;
  padding: 20rpx 16rpx;
  box-sizing: border-box;
  position: fixed;
  width: 100%;
  left: 0;
  top: 0;
  input {
    display: flex;
    width: 100%;
    box-sizing: border-box;
    padding-left: 376rpx;
    background-color: white;
    height: 60rpx;
    border-radius: 8rpx;
    font-size: 24rpx;
    margin-right: 20rpx;
  }
  icon {
    position: absolute;
    //父盒子
    left: 50%;
    top: 50%;
    //自己
    transform: translate(-50%, -50%);
  }
}
//轮播图样式
.swiper-container {
  swiper {
    height: 340rpx;
    .swiper-item {
      height: 100%;
    }
  }
  img {
    display: block;
    width: 100%;
    height: 100%;
  }
}
// 分类的样式
.category-container {
  display: flex;
  padding-top: 24rpx;
  padding: 29rpx;
  background-color: white;
  .item {
    flex: 1;
    img {
      display: block;
      width: 128rpx;
      height: 128rpx;
      margin: 0 auto;
    }
    p {
      text-align: center;
      margin-top: 10rpx;
      font-size: 24rpx;
    }
  }
}
</style>
