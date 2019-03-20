<template>
  <view>
       <!-- 1.0 轮播图模块 -->
    <swiper indicator-dots autoplay circular>
        <block v-for="(item,index) in detail.pics" :key="index">
            <swiper-item>
                <image class="slide-image" mode="aspectFill" :src="item.pics_big_url" @tap="previewBigImage(item.pics_big_url)"></image>
            </swiper-item>
        </block>
    </swiper>
    
     <!-- 2.0 商品价格标题 -->
    <view class="goods-price">
      ￥{{ detail.goods_price }}
    </view>
    <view class="goods-info">
      <view class="info-left">
        {{ detail.goods_name }}
      </view>
      <view class="info-right">
        <view class="iconfont icon-shoucang"></view>
        收藏
      </view>
    </view>
    <!-- 3.0 商品详情图文介绍 -->
    <view class="detail">
       <view class="detail-title">
         商品详情标题
       </view>
       <view class="detail-conent" >
       <!-- 方法一mpvue 提供的解析富文本 -->
         <!-- <view v-html="detail.goods_introduce"></view>  -->
         
         <!-- 方法二原生小程序解析富文本 -->
         <rich-text :nodes="detail.goods_introduce"></rich-text> 
   
       </view>
    </view>

     <!-- 4.0 底部固定条 -->
    <view class="footer">
      <view class="contact">
        <button open-type="contact">打开微信客服聊天</button>
      </view>
      <view class="ft-left">
        <view class="iconfont icon-kefu"></view>
        联系客服
      </view>
      <navigator url="/pages/cart/main" open-type="switchTab" class="ft-left">
        <view class="iconfont icon-gouwuche"></view>
        购物车
      </navigator>
      <view class="ft-right" @tap="addToCart(detail.goods_id)">
        加入购物车
      </view>
      <view class="ft-right">
        立即购买
      </view>
    </view>
  </view>
</template>

<script>

import { getDetail } from "@/api";

export default {
  data () {
     return{
       goods_id:"",
       detail:{},
 
     }
   
  },
  onLoad(query){
    // console.log(query)
     this.goods_id=query.id;
    //  console.log(this.goods_id);
      getDetail({
        goods_id:this.goods_id
      }).then(res=>{
      //  console.log(res);
         this.detail = res.data.message;
        //  console.log(this.detail)
      })
   },
  methods:{
    previewBigImage(current){
      let imgUrls=[];
      this.detail.pics.forEach(item=>{
        imgUrls.push(item.pics_big_url);
      });

      wx.previewImage({
         current: current, // 当前显示图片的http链接
         urls: imgUrls // 需要预览的图片http链接列表
     })
   },
   addToCart(id){
    // 如果没有获取id数据
     if(!id) return;
    //  console.log(id)
  //  console.log(this.detail)
     wx.showToast({
       title: '添加成功',
       icon: 'success',
       duration: 1000,
       mask:true,
   });
    // 2.0.3 获取本地存储中购物车列表数据
     const cartList = wx.getStorageSync("cartList") || {};
     console.log(cartList);
    // 2.0.4 分两种情况
    if(cartList[id]){
       //  2.0.4.1 如果本地存在数据，在原有的 count 上数量 +1
      console.log("1"+cartList[id]);
      cartList[id].count++;
     
    }else{
       //  2.0.4.2 假如没有存放商品的记录，count 设为 1
       cartList[id]=this.detail
       cartList[id].count=1
       console.log("2"+cartList)
    }
       // 2.0.5 添加或修改选中状态
       cartList[id].selected=true;
       // 2.0.6 保存到本地存储
       wx.setStorageSync('cartList',cartList)
   },
 }
  
 
}
</script>

<style lang="scss">
swiper{
    height:720rpx;

    image{
        height:720rpx;
        width:750rpx;
    }
}



.goods-price{
    padding:20rpx;
    color:red;
    font-size:22px;
}

.goods-info{
    padding:20rpx;
    padding-top:0;
    display: flex;

    .info-left{
      flex:1;
      display: -webkit-box;
      -webkit-box-orient: vertical;
      -webkit-line-clamp: 2;
      overflow: hidden;
    }
    .info-right{
        width:160rpx;
        flex-shrink: 0;
        text-align: center;
        color:#999;
        border-left:1px #999 solid;
        font-size:14px;
        margin-left:20rpx;

        display: flex;
        flex-direction: column;
        justify-content: center;
        flex-shrink: 0;
        // 修改字体图标大小
        .icon-shoucang{
          font-size:44rpx;
        }
    }
}

.detail{
    border-top:20rpx #eee solid;
    padding-bottom:120rpx;
    .detail-title{
        padding:20rpx;
        border-bottom:1px #eee solid;
    }
    .detail-content{
      // 父级字号设置为0，清除富文本图片之间的默认间距
      font-size: 0;
    }
}

.footer{
    position: fixed;
    width:100%;
    left:0;
    bottom:0;
    height:100rpx;
    background:#fff;
    display: flex;

    .contact{
        width:20%;
        height:100rpx;
        padding:0;
        margin:0;
        position: absolute;
        left:0;
        top:0;
        // 隐藏真正的客服聊天按钮
        opacity: 0;
    }

    .ft-left{
        width:20%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        color:#666;
        font-size: 14px;

        .iconfont{
            font-size:18px;
        }
    }

    .ft-right{
        width:30%;
        background: orange;
        line-height: 100rpx;
        text-align: center;
        color:#fff;

        &:last-child{
            background: red;
        }
    }

}
</style>
