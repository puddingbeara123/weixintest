<template>
  <view>
    <!-- 1.搜索导航 -->
    <!-- <navigator class="searchInput" hover-class="none"  url="../pages/search/main">
      <view class="search-in">
        <icon type="search" class="search-icon" size="20"/>搜索
      </view>
    </navigator> -->
    <app-search></app-search>

    <!-- 2.0轮播图 -->
    <swiper
  indicator-dots
  autoplay
  interval="2000"
  duration="1000"
  circular
  indicator-color="rgba(255,255,255,0.5)"
  indicator-active-color="#F8F9F9">
  <block v-for="(item,index) in imgUrls" :key="index">
    <swiper-item>
      <image :src="item.image_src" class="slide-image" mode="aspectfill"></image>
    </swiper-item>
  </block>
</swiper>
   <!-- 3.0 首页分类入口 -->
   <view class="nav-bar">
      <block
      v-for="(item,index) in cate"  :key="index">
      <image
        :src="item.image_src" class="nav-image"
        mode="aspectfill">
      </image>
      </block>
   </view>
   <!-- 4.0 楼层 -->
   <block v-for="(item,index) in floor" :key="index">
   <view class="space"></view>
   <view class="floor">
      <view class="floor-title">
        <image 
          :src="item.floor_title.image_src"
         mode="aspectfill">
        </image>
      </view>
      <view class="floor-img">

        <block v-for="(subItem,subIndex) in item.product_list" :key="subIndex">
          <block v-if="subItem.image_width==='232'">
        <view class="imgLeft" >
          <navigator :url="subItem.navigator_url" :open-type="open_type" hover-class="none">
          <image  :src="subItem.image_src" mode="aspectfill"></image>
          </navigator>
        </view>
           </block>
        </block>
        
        <view class="buju">
        <block v-for="(subItem,subIndex) in item.product_list" :key="subIndex" >
        <block v-if="subItem.image_width!=='232'" >
        <view class="imgRight">
          <navigator
            :url="subItem.navigator_url"
            :open-type="subItem.open_type"
            hover-class="none">
          </navigator>
          <image :src="subItem.image_src" mode="aspectfill">
          </image>
        </view>
        </block>
        </block>
      </view>
      </view>
   </view>
   </block>
  </view>
  

</template>

<script>
// 引入组件
import Search from "../../components/Search";

export default {
 data: {
    imgUrls: [],
    cate:[],
    floor:[]
  },
  components:{
    "app-search":Search,
  },
  onLoad(){
    // console.log("123")
    // 轮播图
    wx.request({
        url: "https://zhengzhicheng.cn/api/public/v1/home/swiperdata",
        success: (res) => {
          // console.log(res);
           this.imgUrls= res.data.message;  
        }
 })
//  导航栏
   wx.request({ 
        url: "https://zhengzhicheng.cn/api/public/v1/home/catitems",
        success: (res) => {
          // console.log(res);
           this.cate= res.data.message;  
        }
 })
//  楼层
   wx.request({ 
        url: "https://zhengzhicheng.cn/api/public/v1/home/floordata",
        success: (res) => {
          console.log(res);
          this.floor= res.data.message; 
          // console.log(this.floor.product_list);
         
        }
 })
  }
};
</script>

<style >
.searchInput{
  background-color: #ff2d4a;
  padding:20rpx;
}
.search-in {
  height: 60rpx;
  line-height: 60rpx;
  font-size:36rpx;
  display: flex;
  background-color: #fff;
  justify-content: center;
  align-items: center;
  border: 1rpx solid #ff2d4a;
  border-radius: 10rpx;
  color: #666;
}
.search-icon {
  margin-right: 10rpx;
  margin-top: 30rpx;
}
swiper-item image{
width:750rpx;
height:340rpx;
}
.nav-image{
  width:128rpx;
  height:140rpx;
}
.nav-bar{
  display:flex;
  justify-content: space-around;
  align-items: center; 
  padding:15rpx 0rpx;
}
.floor-title image{
  width:750rpx;
  height:59rpx;
  background-color: #f4f4f4;
}
.space{
  width:750rpx;
  height:30rpx;
 background-color: #f4f4f4;
}
.floor-img{
  display: flex;
  /* justify-content: space-between; */
  padding: 10rpx 0 10rpx 20rpx;
  box-sizing:border-box;
  
}
.imgLeft image{
  height:386rpx;
  width:232rpx;
  margin-right:10rpx;
}
.imgRight image{
  height:188rpx;
   width:233rpx; 
  margin-right:10rpx;
  /* flex:1; */
 
}
.buju{
 
  flex-wrap: wrap;
  display:flex; 
 
 
} 

</style>
