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

      <block v-for="(item,index) in goodsDetail" :key="index" >
       <view class="box">
         <image :src="item.goods_small_logo"></image>
         <view class="box-right">
            <view class="title">{{item.goods_name}}</view>
            <view class="price">￥<text>{{item.goods_price}}.00</text></view>
         </view>
      </view>
     </block>
     
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
     goodsDetail:[],
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
       this.goodsDetail=res.data.message.goods
       console.log(this.goodsDetail);

     })

  },
  methods:{
   changeTabs(index){
     this.tabIndex=index;
   }
  },
  // filters: {
  //   tofixed: function(val) {
  //     return Number(val).toFixed(2);
  //   }
  // }
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
    .price{
      color:#ff2d4a;
    }
  }
}
</style>
