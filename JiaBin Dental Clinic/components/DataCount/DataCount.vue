<template>
  <view class="u-demo">
    <u-cell-group title-bg-color="rgb(243, 244, 246)" :title="item.groupName" v-for="(item, index) in list" :key="index">
      <u-cell-item :titleStyle="{fontWeight: 500}" @click="openPage(item1.path)" v-for="(item1, index1) in item.list"
        :key="index1">
        <work-data></work-data>
      </u-cell-item>
    </u-cell-group>
  </view>
</template>

<script>
import WorkData from '../../components/WorkData/WorkData.vue'
export default {
  data () {
    return {
      mode: 'circle',
      text: '', // 优先级比src高
      size: '90',
      list: [{
        groupName: '作业提交情况',
        list: [{
          path: '/pages/TeaStuAllWork/TeaStuAllWork',
          icon: 'form',
          title: '小刘'
        }, {
          path: '/pages/TeaStuAllWork/TeaStuAllWork',
          icon: 'form',
          title: '小李'
        }, {
          path: '/pages/TeaStuAllWork/TeaStuAllWork',
          icon: 'form',
          title: 's2'
        }, {
          path: '/pages/TeaStuAllWork/TeaStuAllWork',
          icon: 'form',
          title: 's2'
        }]
      }]
    }
  },
  components: {
    WorkData
  },
  computed: {
    getIcon () {
      return path => {
        return 'https://cdn.uviewui.com/uview/example/' + path + '.png'
      }
    }
  },
  methods: {
    openPage (path) {
      uni.redirectTo({
        url: path
      })
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
