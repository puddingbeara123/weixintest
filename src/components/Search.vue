<<template>
    <!-- 1.搜索导航 -->
    <navigator class="searchInput" hover-class="none"  url="../pages/search/main">
      <view class="search-in">
        <icon type="search" class="search-icon" size="20"/>搜索
      </view>
    </navigator>

</template>

<script>
export default {

}
</script>

<style>
.searchInput{
  background-color: #ff2d4a;
  padding:20rpx;
}
.search-in {
  height: 60rpx;
  line-height: 60rpx;
  font-size:36rpx;
  display: flex;
  background-color: #fff;
  justify-content: center;
  align-items: center;
  border: 1rpx solid #ff2d4a;
  border-radius: 10rpx;
  color: #666;
}
.search-icon {
  margin-right: 10rpx;
  margin-top: 30rpx;
}
</style>
