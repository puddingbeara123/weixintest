<template>
  <view>
    <!-- 1.搜索导航 -->
    <navigator class="searchInput" url="pages/search/main">
      <view class="search-in">
        <icon type="search" class="search-icon" size="20"/>搜索
      </view>
    </navigator>

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
      <image :src="item" class="slide-image" mode="aspectfill"></image>
    </swiper-item>
  </block>
</swiper>
   <!-- 3.0 首页分类入口 -->
   <view class="nav-bar">
      <block
      v-for="(item,index) in cate"  :key="index">
      <image
        :src="item" class="nav-image"
        mode="aspectfill">
      </image>
         
      </block>
   </view>
   <!-- 4.0 楼层 -->
   <view class="space"></view>
   <view class="floor">
      <view class="floor-title">
        <image 
          src="https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/pic_floor01_title.png"
         mode="aspectfill">
        </image>
      </view>
      <view class="floor-img">
        <view class="imgLeft">
          <image
            src="https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/pic_floor01_1@2x.png"
             mode="aspectfill">
          </image>
        </view>
        <view class="imgRight">
          <image
            src="https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/pic_floor01_2@2x.png"
             mode="aspectfill">
          </image>
           <image
            src="https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/pic_floor01_3@2x.png"
             mode="aspectfill">
          </image>
           <image
            src="https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/pic_floor01_4@2x.png"
             mode="aspectfill">
          </image>
           <image
            src="https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/pic_floor01_5@2x.png"
             mode="aspectfill">
          </image>
        </view>
      </view>
   </view>

  <view class="space"></view>
   <view class="floor">
      <view class="floor-title">
        <image 
          src="https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/pic_floor01_title.png"
         mode="aspectfill">
        </image>
      </view>
      <view class="floor-img">
        <view class="imgLeft">
          <image
            src="https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/pic_floor01_1@2x.png"
             mode="aspectfill">
          </image>
        </view>
        <view class="imgRight">
          <image
            src="https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/pic_floor01_2@2x.png"
             mode="aspectfill">
          </image>
           <image
            src="https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/pic_floor01_3@2x.png"
             mode="aspectfill">
          </image>
           <image
            src="https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/pic_floor01_4@2x.png"
             mode="aspectfill">
          </image>
           <image
            src="https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/pic_floor01_5@2x.png"
             mode="aspectfill">
          </image>
        </view>
      </view>
   </view>

<view class="space"></view>
   <view class="floor">
      <view class="floor-title">
        <image 
          src="https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/pic_floor01_title.png"
         mode="aspectfill">
        </image>
      </view>
      <view class="floor-img">
        <view class="imgLeft">
          <image
            src="https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/pic_floor01_1@2x.png"
             mode="aspectfill">
          </image>
        </view>
        <view class="imgRight">
          <image
            src="https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/pic_floor01_2@2x.png"
             mode="aspectfill">
          </image>
           <image
            src="https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/pic_floor01_3@2x.png"
             mode="aspectfill">
          </image>
           <image
            src="https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/pic_floor01_4@2x.png"
             mode="aspectfill">
          </image>
           <image
            src="https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/pic_floor01_5@2x.png"
             mode="aspectfill">
          </image>
        </view>
      </view>
   </view>

  </view>
  
  
  
</template>

<script>
export default {
 data: {
    imgUrls: [
      'https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/banner1.png',
      'https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/banner2.png',
      'https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/banner3.png'
    ],
    cate:[
     "https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/icon_index_nav_4@2x.png",
     "https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/icon_index_nav_3@2x.png",
     "https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/icon_index_nav_2@2x.png",
     "https://lg-igjc8p1o-1256763078.cos.ap-shanghai.myqcloud.com/upload/icon_index_nav_1@2x.png"
    ]
  },
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
  padding:10rpx 0rpx 10rpx 16rpx;
}
.imgLeft image{
  height:386rpx;
  width:232rpx;
  margin-right:12rpx;
}
.imgRight image{
  height:188rpx;
  width:233rpx;
    margin-right:12rpx;
}
</style>
