<template>
  <view>
    <wechat-data></wechat-data>
    <u-cell-group title-bg-color="rgb(243, 244, 246)" :title="item.groupName" v-for="(item, index) in list" :key="index">
      <u-cell-item :titleStyle="{fontWeight: 500}" @click="openPage(item1.path)" v-for="(item1, index1) in item.list"
        :key="index1">
        <tea-work></tea-work>
      </u-cell-item>
    </u-cell-group>
  </view>
</template>

<script>
import WechatData from '../../components/WechatData/WechatData'
import TeaWork from '../../components/TeaWork/TeaWork'
export default {
  data() {
    return {
      list: [{
        groupName: '该学生已完成作业（可批改）',
        list: [{
          path: '/pages/TeaStuSingleWork/TeaStuSingleWork',
          icon: 'form',
          title: '小刘'
        }, {
          path: '/pages/TeaStuSingleWork/TeaStuSingleWork',
          icon: 'form',
          title: '小李'
        }]
      },
      {
        groupName: '该学生未完成作业(不可查看)',
        list: [{
          path: '',
          icon: 'form',
          title: '小刘'
        }]
      }]
    }
  },
  components: {
    WechatData,
    TeaWork
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

<style>

</style>
