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

   <!-- 综合 -->
   <view class="goodsDetail">
     <!-- <block v-for="(item,index) in goodsDetail" :key="index" > -->
       <view class="box">
         <image src="http://image4.suning.cn/uimg/b2c/newcatentries/0000000000-000000000152287756_2_200x200.jpg"></image>
         <view class="box-right">
            <view class="title">小米（MI）米家压力IH电饭煲 智能烹饪 压力IH电磁环绕加热 手机智能预约 3L黄金容量 灰铸铁内胆</view>
            <view class="price">￥<text>221{{ssss| tofixed}}</text></view>
            
         </view>
      </view>
     <!-- </block> -->
     

   </view>
     
  </view>
   
</template>

<script>
// 引入组件
import request from "../../utils/request";

export default {
 data() {
    return {
     keyword:"",
     tabItem:["综合","销量","价格"],
     tabIndex:0,
    }
  },
  onLoad(option){
   
    console.log(option.keyword)
     this.keyword=option.keyword;
     const data={
      query: this.keyword
     }
    //  console.log(data)
     request("https://www.zhengzhicheng.cn/api/public/v1/goods/search", data).then((res)=>{
       console.log(res);
     })

  },
  methods:{
   changeTabs(index){
     this.tabIndex=index;
   }
  },
    filters: {
    tofixed: function(data) {
      return Number(data).toFixed(2);
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
.box{
  display:flex;
  image{
    width:220rpx;
    height:220rpx;
    margin:20rpx;
    flex-shrink: 0;
  }
  .box-right{
    flex:1;
    .title{
      overflow:hidden;
      text-overflow:ellipsis;
     display:-webkit-box; 
    -webkit-box-orient:vertical;    
    -webkit-line-clamp:2; 
    margin:20rpx;
    }
  }
}
</style>
