<template>
  <view>
    <app-search></app-search>
    <view class="section secLeft">
      <scroll-view
        scroll-y
        style="height: 200px;"
        bindscrolltoupper="upper"
        bindscrolltolower="lower"
        bindscroll="scroll"
        scroll-into-view="red"
        scroll-top="100">
        <block></block>
        <view id="green" class="scroll-view-item bc_green">大家电</view>
        <view id="red" class="scroll-view-item bc_red">热门推荐</view>
        <view id="yellow" class="scroll-view-item bc_yellow">海外购</view>
        <view id="blue" class="scroll-view-item bc_blue">苏宁房产</view>
      </scroll-view>
    </view>
    
  </view>
</template>

<script>
// 引入组件
import Search from "../../components/Search";

export default {
  data:{
     toView: 'red',
    scrollTop: 100,
  },
  components: {
    "app-search": Search
  }
};
</script>

<style>
.secLeft{
  width:196rpx;
  background-color: #f5f5f4;
  color:#323332;
  font-size:40rpx;
}

</style>
