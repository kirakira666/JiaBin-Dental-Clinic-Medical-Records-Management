<template>
  <view>
    <u-subsection :current=Inv :list="['普通作业', '考试','相册']" @change="modeChange"></u-subsection>
    <view>
      <text>进行中</text>
      <stu-work></stu-work>
      <text>已截止</text>
      <stu-work></stu-work>
    </view>
  </view>
</template>

<script>
  import StuWork from '../../components/StuWork/StuWork.vue'
  export default {
    data() {
      return {
        Inv: 1,
        path: [
          '/pages/CommonWork/CommonWork',
          '/pages/StuTest/StuTest',
          '/pages/ClassPhoto/ClassPhoto'
        ]
      }
    },
    components: {
      StuWork,
    },
    methods: {
      modeChange (index) {
        this.Inv = index
        uni.redirectTo({
          url: this.path[index]
        })
      }
    }
  }
</script>

<style>

</style>
