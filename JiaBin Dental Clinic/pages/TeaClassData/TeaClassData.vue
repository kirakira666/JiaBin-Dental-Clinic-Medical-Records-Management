<template>
  <view class="u-demo">
    <u-button type="default" open-type="share">邀请学生进班</u-button>
    <u-button @click="toCode">查看班级二维码</u-button>
    <u-subsection :current=Inv :list="['成员', '统计', '作业', '相册']" @change="modeChange"></u-subsection>
    <view v-show="Inv === 0 ">
      <members></members>
    </view>
    <view v-show="Inv === 1 ">
      <data-count ></data-count>
    </view>
    <view v-show="Inv === 2 ">
      <tea-all-work ></tea-all-work>
    </view>
    <view v-show="Inv === 3 ">
      <class-photo></class-photo>
    </view>
  </view>
</template>

<script>
import Members from '../../components/Members/Members.vue'
import DataCount from '../../components/DataCount/DataCount.vue'
import TeaAllWork from '../../components/TeaAllWork/TeaAllWork.vue'
import ClassPhoto from '../../components/ClassPhoto/ClassPhoto.vue'
export default {
  data () {
    return {
      Inv: 0,
      title: '班级信息',
      mode: 'circle',
      text: '', // 优先级比src高
      size: '90',
    }
  },
  computed: {
    getIcon () {
      return path => {
        return 'https://cdn.uviewui.com/uview/example/' + path + '.png'
      }
    }
  },
  components: {
    Members,
    DataCount,
    TeaAllWork,
    ClassPhoto
  },
  methods: {
    changeTab (Inv) {
      that.navIdx = Inv
    },
    modeChange (index) {
      this.Inv = index
    },
    toCode () {
      this.$u.route({
        url: 'pages/Code/Code'
      })
    },
    onShareAppMessage (res) {
      if (res.from === 'button') {
        return {
          title: '邀请进班',
          path: '/pages/Members/Members',
          imageUrl: '../../static/class.png'
        }
      }
    }
  }
}
</script>

<style lang="scss" scoped>
  .u-cell-icon {
    height: 40rpx;
    width: 40rpx;
  }
</style>
