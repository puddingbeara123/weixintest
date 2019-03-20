<template>
  <view>
    <app-search></app-search>
  
    <view class="scrollAll">

      <scroll-view   scroll-y class="scrollLeft">
        <block v-for="(item,index) in scrollLeftdata" :key="index">
          <view class="item" :class="{ active : index === tabIndex }" @tap="changeTabs(index)">{{item.cat_name}}</view>
        </block>
      </scroll-view>

      <scroll-view  scroll-y class="scrollRight">
        <block v-for="(item,index) in scrollRightData" :key="index">
           <view class="scrollRight-title">{{item.cat_name}}</view>
           <view class="scrollRight-list">
             <block v-for="(subItem,subIndex) in item.children" :key="subIndex">
              <view class="scrollRight-list-item" @tap="gotoGoodList(subItem.cat_name)">
                  <image class="scrollRight-image" :src="subItem.cat_icon"></image>
                  <view>{{subItem.cat_name}}</view>
              </view>
             </block>
           </view>
         </block>
      </scroll-view>


    </view>
    
  </view>
</template>

<script>
// 引入组件
import Search from "../../components/Search";
import request from "../../utils/request";
// console.log(request)

export default {
  data(){
    return{
        tabIndex: 0,
        scrollLeftdata:[],
        scrollRightData:[]

    }
  },
  onLoad(){
    wx.showLoading({
     title: '客官稍等~',
    }),
    request("https://www.zhengzhicheng.cn/api/public/v1/categories").then((res)=>{
      // console.log(res);
      this.scrollLeftdata=res.data.message; //渲染左边的菜单栏
        // console.log(this.scrollLeftdata); 
        this.scrollRightData=this.scrollLeftdata[this.tabIndex].children;//渲染右边的子菜单
        console.log(this.scrollRightData);
         wx.hideLoading();
    })
  },

  components: {
    "app-search": Search
  },
  methods:{
    // 点击左边的菜单栏带动右边的子菜单显示
      changeTabs(index){
      this.tabIndex = index;
      this.scrollRightData=[];//先清空右侧的菜单栏
      setTimeout(()=>{  // 2. 赋值阶段，利用定时器让数据清空后再赋值
        this.scrollRightData=this.scrollLeftdata[this.tabIndex].children;
      },0)
    },
    gotoGoodList(name){
       wx.navigateTo({url:'/pages/goodList/main?keyword='+name})
    }
  }
};
</script>

<style>
.searchInput{
   position: fixed;
   width:100%;
   box-sizing: border-box;
}
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
