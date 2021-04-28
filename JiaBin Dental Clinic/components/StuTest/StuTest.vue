<template>
  <view>
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
      }
    },
    components: {
      StuWork,
    },
    methods: {
    }
  }
</script>

<style>

</style>
