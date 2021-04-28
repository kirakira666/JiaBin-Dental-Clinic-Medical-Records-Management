<template>
  <view class="">
    <view class="u-card-wrap">
      <u-card @head-click="headClick" :title="title" :sub-title="releaseTime" :padding="padding" :border="border">
        <view class="" slot="body">
          <view class="u-body-item-title u-line-2"  @click="click">
            分享到：
            <uni-icons type="weixin" class="icon" size="20" color="rgb(143,143,148)"></uni-icons>
            <uni-icons type="pengyouquan" class="icon" size="20" color="rgb(143,143,148)"></uni-icons>
            <uni-icons type="qq" class="icon" size="20" color="rgb(143,143,148)"></uni-icons>
          </view>
        </view>
      </u-card>
    </view>
  </view>
</template>

<script>
export default {
  data () {
    return {
      title: '作业名称发广告恢复工具方式如果各位大噶阿凡达',
      releaseTime: '2020-05-15',
      padding: 20,
      bottomSlot: true,
      border: true
    }
  },
  methods: {
    click (index) {
      console.log('分享')
    },
    headClick (index) {
      console.log('查看详情')
      this.$u.route({
        url: 'pages/TeaWorkAllStu/TeaWorkAllStu'
      })
    }
  }
}
</script>

<style scoped lang="scss">
  .u-demo {
    padding-top: 50px;
  }

  .u-card-wrap {
    background-color: $u-bg-color;
    padding: 1px;
  }

  .u-body-item {
    font-size: 32rpx;
    color: #333;
    padding: 20rpx 10rpx;
  }

  .u-body-item image {
    width: 120rpx;
    flex: 0 0 120rpx;
    height: 120rpx;
    border-radius: 8rpx;
    margin-left: 12rpx;
  }

  .icon {
    float: right;
    margin: 5rpx;
  }
</style>
