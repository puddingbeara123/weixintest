<template>
  <view>
    <navigator class="searchInput" src="pages/search/main">
      <view class="search-in">
        <icon type="search" class="search-icon" size="20"/>搜索
      </view>
    </navigator>
    <swiper
  indicator-dots
  autoplay
  interval="2000"
  duration="1000"
  circular
  indicator-color="rgba(255,255,255,0.3)"
  ndicator-active-color="rgba(255,255,255,1)"

>
  <block>
    <swiper-item>
      <image src="{{item}}" class="slide-image" width="355" height="150" />
    </swiper-item>
  </block>
</swiper>
  </view>
</template>

<script>
export default {
  data() {}
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
</style>
