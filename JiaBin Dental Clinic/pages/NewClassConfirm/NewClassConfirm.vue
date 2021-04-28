<template>
  <view class="u-demo">
    <view class="u-demo-wrap">
      <u-cell-group title-bg-color="rgb(243, 244, 246)" title="信息确认:">
        <u-cell-item :arrow="false" :titleStyle="{fontWeight: 500}" title="姓名:" :value="params.name"></u-cell-item>
        <u-cell-item :arrow="false" :titleStyle="{fontWeight: 500}" title="性别:" :value="params.classType"></u-cell-item>
        <u-cell-item :arrow="false" :titleStyle="{fontWeight: 500}" title="主治医师:" :value="params.courseType"></u-cell-item>
        <u-cell-item :arrow="false" :titleStyle="{fontWeight: 500}" title="是否初诊:" :value="params.isFirst"></u-cell-item>
        <u-cell-item :arrow="false" :titleStyle="{fontWeight: 500}" title="电话号码:" :value="params.phone"></u-cell-item>
      </u-cell-group>
      <u-toast ref="uToast" />
      <view class="u-demo-area">
        <view class="u-btn-wrap">
          <u-button type="primary" @click="confirm">确认</u-button>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        params: {}
      }
    },
    onLoad(option) {
      this.params = option
    },
    methods: {
      confirm () {
        uni.redirectTo({
          url: '/pages/TeaClassList/TeaClassList'
        })
      }
    }
  }
</script>

<style lang="scss" scoped>
  .wrap {
    padding: 24rpx;
  }

  .u-btn-wrap {
    margin-top: 50rpx;
  }
</style>
