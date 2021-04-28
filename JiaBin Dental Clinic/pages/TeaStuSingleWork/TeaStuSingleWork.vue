<template>
  <view>
    <view class="">
      <text>作业标题：{{homeworkTitle}}</text>
    </view>
    <view class="">
      <text>截止时间：{{deadline}}</text>
    </view>
    <work-data></work-data>
    <u-cell-group title-bg-color="rgb(243, 244, 246)" :title="item.groupName" v-for="(item, index) in list" :key="index">
      <u-cell-item :titleStyle="{fontWeight: 500}" @click="openPage(item1.path)" v-for="(item1, index1) in item.list"
        :key="index1">
        <problem-list></problem-list>
      </u-cell-item>
    </u-cell-group>
  </view>
</template>

<script>
import WechatData from '../../components/WechatData/WechatData'
import WorkData from '../../components/WorkData/WorkData'
import ProblemList from '../../components/ProblemList/ProblemList'
export default {
  data() {
    return {
      homeworkTitle: '7月16日第一次作业',
      deadline: '7月16日15：00',
      list: [{
        groupName: '题目列表',
        list: [{
          path: '/pages/AddFeedback/AddFeedback'
        }, {
          path: '/pages/AddFeedback/AddFeedback'
        }, {
          path: '/pages/AddFeedback/AddFeedback'
        }]
      }]
    }
  },
  components: {
    WechatData,
    WorkData,
    ProblemList
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
