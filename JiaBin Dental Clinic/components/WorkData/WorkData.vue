<template>
  <view class="workdata">
    <u-avatar class="avatar"></u-avatar>
    <view class="txt">
      <text>学生姓名</text>
    </view>
   <text class="txt">已交0次</text>
    <text class="txt">未完成0次</text>
  </view>
</template>

<script>
export default {
  data () {
    return {

    }
  }
}
</script>

<style scoped>
  .workdata {
    padding: 0rpx;
    border: 1rpx solid #FFFFFF;
    font-size: 30rpx;
  }
  
  .avatar {
    display: inline;
  }
  
  .txt {
    width: 1000rpx;
    margin: 40rpx;
    display: inline;
  }

  .navi {
    margin-left: 40rpx;
    display: inline;
  }
</style>
