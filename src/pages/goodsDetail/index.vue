<template>
  <view>
   商品详情页{{goods_id}}
  </view>
</template>

<script>


export default {
  data () {
     return{
       goods_id:""
     }
   
  },
  onLoad(query){
    console.log(query);
     this.goods_id=query.id;
   }
 
}
</script>

<style>

</style>
