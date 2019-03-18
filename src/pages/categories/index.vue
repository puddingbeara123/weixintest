<template>
  <view>
    <app-search></app-search>
  
    <view class="scrollAll">
      <view class="scrollLeft">
        <block v-for="(item,index) in [1,2,3,1,4,5,4,4,7,5,7,9,7,5,4,1,4,5,2]" :key="index">
          <view class="item" :class="{ active : index === tabIndex }" @tap="changeTabs(index)">大家电</view>
        </block>
      </view>
      <view class="scrollRight">
        <view class="scrollRight-title">电视机</view>
         <view class="scrollRight-list">
          <block v-for="(item,index) in [1,2,3,1,4,5,4,4,7,5,7,9,7,5,4,1,4,5,2]" :key="index">
              <view class="scrollRight-list-item">
                  <image class="scrollRight-image" src="https://img.alicdn.com/imgextra/i4/17971277/O1CN011LIuFRe38gnZqZl_!!0-saturn_solar.jpg_220x220.jpg_.webp"></image>
                  <view>分类名称</view>
              </view>
         </block>
        </view>
      </view>
    </view>
    
  </view>
</template>

<script>
// 引入组件
import Search from "../../components/Search";
import request from "../../utils/request";
console.log(request)

export default {
  data(){
    return{
        tabIndex: 0
    }
  },
  onLoad(){
    request("https://www.zhengzhicheng.cn/api/public/v1/categories").then((res)=>{
      console.log(res);
    })
  },

  components: {
    "app-search": Search
  },
  methods:{
      changeTabs(index){
      this.tabIndex = index;
    }
  }
};
</script>

<style>
.scrollAll{
  display:flex;
  position:fixed;
  left:0;
  right:0;
  top:100rpx;
  bottom:0;
}
.scrollLeft{
  width:200rpx;
  flex-shrink:0;
  height:100%;
  background-color: #f4f4f4;
}
.scrollRight{
  flex:1;
}
.scrollLeft .item{
  border-bottom:1rpx solid #eeeeee;
  color:black;
  font-size:36rpx;
  line-height:100rpx;
  text-align: center;
  position: relative;
 
}
.scrollLeft .item.active{
  background-color: #fff;
  color:#ff2d4a;

}
  

 .scrollRight-image {
  width:140rpx;
  height:140rpx;
} 
.scrollRight-list{
  display:flex;
   flex-wrap: wrap;
}
.scrollRight-list-item{
  width: 33.33%;
  font-size: 30rpx;
  text-align: center;
  padding: 20rpx 0;
}
.scrollRight-title{
  text-align:center;
    padding: 30rpx 0;
}
.scrollRight-title::after,
.scrollRight-title::before{
  content: "/";
  color:#ccc;
  margin: 0 20rpx;
}
 .scrollLeft .item.active::after{
  /* display:block; */
  content:"";
  position: absolute;
  width: 10rpx;
  background-color: #ff2d4a;
  left: 0;
  top:15rpx;
   bottom:15rpx;                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              
} 

</style>
