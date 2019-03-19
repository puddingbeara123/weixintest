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

   <!-- 没有数据的提示 -->
   <view class="loading" v-show="!hasMore">到底了...</view>
     
  </view>
   
</template>

<script>
// 引入组件
import { getSearch } from "@/api/index";
// console.log(getSearch);

export default {
 data() {
    return {
     keyword:"",
     tabItem:["综合","销量","价格"],
     tabIndex:0,
     goodsDetail:[],
     pagenum:1,
     pagesize:20,
     hasMore: true
    }
  },
  onLoad(option){
     this.keyword=option.keyword;
     this.getData();
  },
  onUnload(){
    this.initData()
  },
  methods:{
    // 切换tab栏
   changeTabs(index){
     this.tabIndex=index;
   },
     //  渲染数据封装
   getData(){
    //  还没有到底的时候，要隐藏
     if(!this.hasMore) return;
     wx.showLoading({
       title: '加载中...',
      })
     getSearch({
        query: this.keyword,
        pagenum: this.pagenum,
        pagesize: this.pagesize
     }).then(res =>{
       let { goods } = res.data.message;
      //  console.log(goods);
        this.goodsDetail = [...this.goodsDetail,...goods];

        this.pagenum++;

        if(goods.length<this.pagesize){
          this.hasMore = false;
        }
        // 数据加载完成后，隐藏加载框
          wx.hideLoading()
        // 把下拉刷新动画页停止
         wx.stopPullDownRefresh();

     })
   },
   // 初始化 data 数据
   initData(){
     this.pagenum = 1;
     this.hasMore = true;
     this.goodsDetail=[];
   }
  },
  onPullDownRefresh(){
    //  6.0.1 初始化页面数据
    this.initData();
      //  6.0.2 重新请求数据
    this.getData();
  },
   // 页面触底事件
  onReachBottom(){
        // 页面触底的时候页调用获取数据的函数
    this.getData();
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
    .price{
      color:#ff2d4a;
    }
  }
}
.loading{
   line-height: 80rpx;
    text-align: center;
    font-size:14px;
    color:#999;
}
</style>
