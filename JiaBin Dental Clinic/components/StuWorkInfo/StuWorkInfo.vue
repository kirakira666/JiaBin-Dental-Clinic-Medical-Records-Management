<template>
  <view class="info">
    <u-avatar></u-avatar>
    <text class="txt">学生姓名</text>
    <text class="txt">已提交</text>
    <!-- <text class="txt">未提交</text> -->
    <button @click="toTeaStuSingleWork" class="btn">查看作业</button>
    <!-- <button class="btn">提醒分享</button> -->
  </view>
</template>

<script>
export default {
  data () {
    return {
    };
  },
  methods: {
    toTeaStuSingleWork () {
      this.$u.route({
        url: 'pages/TeaStuSingleWork/TeaStuSingleWork'
      })
    }
  }
}
</script>

<style scoped>
  .info {
    padding: 0rpx;
    border: 1rpx solid #FFFFFF;
    font-size: 30rpx;
  }

  .txt {
    display: inline;
    margin: 0rpx 35rpx;
  }

  .btn {
    display: inline;
    margin-left: 35rpx;
    font-size: 30rpx;
  }
</style>
