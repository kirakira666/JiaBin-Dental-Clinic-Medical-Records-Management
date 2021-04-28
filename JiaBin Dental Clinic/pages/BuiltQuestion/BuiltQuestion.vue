<template>
  <view class="u-demo">
    <view class="u-config-wrap">
      <view class="u-demo-title">课程名称：{{title}}</view>
      <u-button @click="NewQuestionClick">添加题目</u-button>
    </view>
    <u-cell-group title-bg-color="rgb(243, 244, 246)" :title="item.groupName" v-for="(item, index) in list" :key="index">
      <u-cell-item :titleStyle="{fontWeight: 500}" @click="openPage(item1.path)" :title="item1.title" v-for="(item1, index1) in item.list"
        :key="index1">
        <image slot="icon" class="u-cell-icon" :src="getIcon(item1.icon)" mode="widthFix"></image>
      </u-cell-item>
    </u-cell-group>
  </view>
</template>

<script>
export default {
  data () {
    return {
      title: 'XX课程自建题库',
      mode: 'circle',
      text: '', // 优先级比src高
      size: '90',
      list: [{
        groupName: '第一单元',
        list: [{
          path: '',
          icon: 'form',
          title: '第1次作业'
        }]
      },
      {
        groupName: '第二单元',
        list: [{
          path: '',
          icon: 'form',
          title: '第1次作业'
        }, {
          path: '',
          icon: 'form',
          title: '第2次作业'
        }]
      },
      {
        groupName: '测试',
        list: [{
          path: '',
          icon: 'form',
          title: '第1次测试'
        }, {
          path: '',
          icon: 'form',
          title: '第2次测试'
        }]
      }
      ]
    }
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

  .u-demo-title {
    height: 100rpx;
    padding: 30rpx;
  }
</style>
