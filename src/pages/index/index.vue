<template>
 <view>
   <navigator class="searchInput" src="pages/search/main">
    <icon type="search" class="search-icon" size="20"/>
   搜索
   </navigator>
 </view>
</template>

<script>


export default {
  data () {
  
  },

  
}
</script>

<style >
.searchInput{
  height:60rpx;
  line-height: 60rpx;
  display:flex;
  justify-content: center;
  align-items: center;
  border:1rpx solid #ff2d4a;
  border-radius:10rpx;
  color:#666;
}
.search-icon{
  margin-right:10rpx;
}
</style>
