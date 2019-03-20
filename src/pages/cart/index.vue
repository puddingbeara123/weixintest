<template>
  <view>
    <!-- 1.0 顶部地址选择 -->
    <view class="cart-top" @tap="chooseAddressHandle"> 
         <!-- 1.0.1 用户选择了收货地址的时候展示 -->
        <block v-if="address.username">
           <view class="user">
             <text>收货人：{{address.username}}</text>
             <text>{{address.tel}}</text>
           </view>
           <view class="address">
              收货地址：{{ address.addressInfo }}
           </view>
        </block>
        <!-- 1.0.2 用户没选择收货地址的时候，显示添加收货地址 -->
        <block v-else> 
           <view class="add-address">
                <button>+添加收货地址</button>
            </view> 
         </block>
        <view class="address-border"></view>
    </view>

    <!-- 2.0 店铺标题和商品列表 -->
    
    <view class="list-title"><text class="iconfont icon-ziyuan4"></text>优购生活馆</view>
    <view class="ware-list">
        <block v-for="(item,index) in [1,2,3]" :key="index">
        <view class="ware-item">
          <!-- 2.0.2 左边按钮 -->
          <view class="choice-button">
            <view class="iconfont icon-xuanze-fill"></view>
          </view>
          <!-- 2.0.3 右边图片和商品信息 -->
          <view class="ware-content">
             <!-- 2.0.4 图片 -->
             <view class="ware-image">
                <image
                  src="https://img.alicdn.com/simba/img/TB1hP95MQvoK1RjSZFwSuwiCFXa.jpg"
                  mode="aspectFill">
                </image>
             </view>
             <!-- 2.0.5 商品信息 -->
             <view class="ware-info">
                <view class="ware-info-title">
                    商品标题商品标题商品标题商品标题商品标题商品标题商品标题商品标题
                </view>
                <view class="ware-info-btm">
                  <view class="ware-price">
                    ￥<text>999</text>.00
                  </view>
                  <view class="calculate">
                    <view class="rect">-</view>
                    <view class="number">3</view>
                    <view class="rect">+</view>
                  </view>
                </view>
             </view>
          </view>
        </view>
      </block> 
    </view>
    <!-- 3.0 底部固定条 -->
    <view class="cart-total">
      <view class="total-button">
        <view class="iconfont icon-xuanze"></view>全选
      </view>
      <view class="total-center">
        <view>合计:<text class="color-red">￥ 999</text> </view>
        <view class="price-tips">包含运费</view>
      </view>
       <view class="accounts">
        结算(3)
      </view>
    </view>
  </view>
</template>

<script>


export default {
  data () {
    return{
     address:{
        username:"",
        tel:"",
        addressInfo:""
      }
    }
  },
  onShow(){
    this.address = wx.getStorageSync('address') || {};
  },
  methods:{
    chooseAddressHandle(){
       wx.chooseAddress({
        success(res) {
         let{provinceName,cityName,countyName,detailInfo,userName,telNumber}=res;
            // 1.0.3 地址信息数据绑定
           this.address={
             username: userName,
               tel: telNumber,
                addressInfo:`${provinceName}${cityName}${countyName}${detailInfo}`
           } 
           // 1.0.4 添加到本地存储
          wx.setStorageSync('address', this.address);
        }
    });
    }
  }

}
</script>

<style lang="scss">
// 1.0 顶部地址选择
.cart-top {
    min-height: 180rpx;
    position: relative;
    .user {
        display: flex;
        padding: 20rpx;
        justify-content: space-between;
        position: relative;
        padding-right: 50rpx;
        &:after {
            display: block;
            content: "";
            width: 12px;
            height: 12px;
            border-top: 1px #999 solid;
            border-right: 1px #999 solid;
            transform: rotate(45deg);
            position: absolute;
            right: 20rpx;
            top: 20rpx;
            margin-top: 6px;
        }
    }
    .address {
        padding: 20rpx;
        padding-top: 0;
    }
    .address-border {
        width: 100%;
        height: 8px;
        position: absolute;
        bottom: 0;
        left: 0;
        right: 0;
        background-color: red;
    }
    .add-address {
        height: 180rpx;
        padding: 20rpx;
        box-sizing: border-box;
        display: flex;
        justify-content: center;
        align-items: center;
    }
}

// 2.0 页面选择按钮颜色
.icon-xuanze-fill {
    color: #ff2d4a;
}

// 2.0.1 店铺标题和商品列表
.list-title {
    padding: 20rpx;
    border-bottom: 1px #eee solid;
    border-top: 10px #eee solid;
    text{
      margin-right:10rpx;
    }
}

.ware-list {
    padding-bottom: 100rpx;
}

.ware-item {
    padding: 20rpx;
    padding-bottom: 0;
    display: flex;
    align-items: center;

    .choice-button {
        flex-shrink: 0;
        text-align: center;
        margin-right: 20rpx;
        font-size: 32rpx;
    }

    .ware-content {
        display: flex;
        flex: 1;
        justify-content: space-between;
        border-bottom: 1px #eee solid;
        padding-bottom: 20rpx;
    }

    .ware-image {
        image {
            display: block;
            width: 200rpx;
            height: 200rpx;
        }
    }

    .ware-info {
        flex: 1;
        margin-left: 20rpx;
        display: flex;
        flex-direction: column;
        justify-content: space-between;

        .ware-info-title {
            display: -webkit-box;
            -webkit-box-orient: vertical;
            -webkit-line-clamp: 2;
            overflow: hidden;
        }

        .ware-info-btm {
            display: flex;
            justify-content: space-between;
            .ware-price {
                color: red;
            }
            .calculate {
                display: flex;

                .rect {
                    width: 20px;
                    text-align: center;
                    border: 1px #999 solid;
                    line-height: 1.2;
                }
                .number {
                    margin: 0 10px;
                }
            }
        }
    }
}

// 3.0 底部固定条
.cart-total {
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 100rpx;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: #fff;
    .total-button {
        padding-left: 20px;
        display: flex;
        align-items: center;
        .iconfont {
            margin-right: 10px;
        }
    }
    .total-center {
        flex: 1;
        padding: 20rpx;
        text-align: right;
        .color-red {
            color: red;
        }
        .price-tips {
            font-size: 14px;
            color: #666;
        }
    }
    .accounts {
        width: 30%;
        height: 100rpx;
        background: red;
        color: #fff;
        line-height: 100rpx;
        text-align: center;
    }
}
</style>
