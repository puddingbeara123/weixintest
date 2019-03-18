<template>
  <view>
   <!-- 商品搜索框 -->
   <view class="searchWrap">
      <view class="searchInput">
         <icon type="search" class="searchIcon" size="20"/>
         <text>{{keyword}}</text>
      </view>
   </view>
   <!-- tab栏 -->
   <view class="tab">
     <block>
       <view v-for="(item,index) in tabItem" :key="index">
           <view class="tab-item" :class="{active:index == tabIndex}" @tap="changeTabs(index)">{{item}}</view>
       </view>
       </block> 
   </view>
     
  </view>
   
</template>

<script>
// 引入组件


export default {
 data() {
    return {
     keyword:"",
     tabItem:["综合","销量","价格"],
     tabIndex:0
    }
  },
  onLoad(option){
    console.log(option.keyword)
     this.keyword=option.keyword;
     request("")

  },
  methods:{
   changeTabs(index){
     this.tabIndex=index;
   }
  }
};
</script>

<style lang="scss" >
.searchWrap{
   background-color: #eee;
   padding:30rpx 16rpx;
  .searchInput{
    height: 60rpx;
  line-height: 60rpx;
  font-size:40rpx;
  display: flex;
  background-color: #fff;
  align-items: center;
  border-radius: 10rpx;
  color:black;
    .searchIcon{
      color:#ddd;
      margin-right:20rpx;
      margin-top:30rpx;
    }
  }
}
.active{
  color:#ff2d4a;
}
.tab{
  border-bottom:1rpx solid #ddd;
  display:flex;
  line-height: 98rpx;
  justify-content: space-around;
}
</style>
