<template>
  <view class="classmember">
    <u-avatar></u-avatar>
    <text class="member">学生姓名</text>
    <navigator url="/pages/StuCenter/StuCenter" hover-class="navigator-hover" class="navileft">查看信息</navigator>
    <navigator url="" class="member">编辑</navigator>
    <navigator url="" class="member">删除</navigator>
    <navigator url="" class="naviright">设置管理员</navigator>
  </view>
</template>

<script>
export default {
  data() {
    return { 
    };
  }
  }
</script>

<style scoped>
  .classmember {
    padding: 0rpx;
    border: 1rpx solid #FFFFFF;
    font-size: 30rpx;
  }
  .navileft {
    display: inline-block;
    margin-left: 20rpx;
    display: inline;
  }
  .member {
    margin: 6rpx;
    display: inline;
   }
  .naviright {
    margin-right: 0rpx;
    margin-left: 2rpx;
    display: inline;
  }
</style>