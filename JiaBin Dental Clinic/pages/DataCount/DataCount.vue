<template>
  <view class="u-demo">
    <view class="u-demo-wrap">
      <view class="u-demo-title">{{title}}</view>
    </view>
    <view class="u-config-wrap">
      <view class="u-config-item">
        <u-subsection vibrateShort current='1' :list="['成员', '统计', '作业', '相册']" @change="modeChange"></u-subsection>
      </view>
    </view>
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
      title: '班级统计',
      mode: 'circle',
      text: '', // 优先级比src高
      size: '90',
      list: [{
        groupName: '作业提交情况',
        list: [{
          path: '/pages/TeaClassList/TeaClassList',
          icon: 'form',
          title: '小刘'
        }, {
          path: '/pages/TeaClassList/TeaClassList',
          icon: 'form',
          title: '小李'
        }, {
          path: '/pages/TeaClassList/TeaClassList',
          icon: 'form',
          title: 's2'
        }, {
          path: '/pages/TeaClassList/TeaClassList',
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
    modeChange (index) {
      console.log('hhhhhh')
      if (index === 0) {
        this.$u.route({
          url: '/pages/Menbers/Menbers'
        })
      } else if (index === 1) {
        this.$u.route({
          url: '/pages/DataCount/DataCount'
        })
      } else if (index === 2) {
        this.$u.route({
          url: '/pages/ClassWork/ClassWork'
        })
      } else if (index === 3) {
        this.$u.route({
          url: '/pages/ClassPhoto/ClassPhoto'
        })
      }
    },
    openPage (path) {
      this.$u.route({
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
