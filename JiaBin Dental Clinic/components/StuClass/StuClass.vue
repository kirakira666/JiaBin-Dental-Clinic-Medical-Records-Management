<template>
  <view class="StuClass" @click="toClass">
    <view>
      <view class="txt"><text>班级名称: 班级123班</text></view>
      <view class="txt"><text>课程名称：中华写字课堂</text></view>
      <view class="txt"><text>任课老师：李华老师</text></view>
    </view>
  </view>
</template>

<script>
export default {
  data () {
    return {
    }
  },
  methods: {
    toClass () {
      this.$emit('toClass')
    }
  }
}
</script>

<style scoped>
  .StuClass {
    border: 1rpx solid #000000;
    font-size: 30rpx;
  }

  .txt {
    margin: 10rpx;
  }

  .btn {
    display: inline-block;
    margin: 40rpx;
    font-size: 30rpx;
  }

</style>
