<template>
  <view>
    <view>
      <text>未提交</text>
      <view v-for="(item, index) in undoneWork" :key=index>
        <u-button type="default" @click="toDo">去完成</u-button>
        <stu-work></stu-work>
      </view>
      <text>已提交（未批改）</text>
      <stu-work></stu-work>
      <text>已批改</text>
      <stu-work></stu-work>
    </view>
  </view>
</template>

<script>
  import StuWork from '../../components/StuWork/StuWork.vue'
  export default {
    data() {
      return {
        undoneWork: [
          {
            name: '作业名称',
          },
          {
            due: '2020-10-9'
          },
        ],
        doneWork: [

        ],
        checkWork: [

        ]
      }
    },
    components: {
      StuWork,
    },
    methods: {
      toDo () {
        console.log('do your work!')
        uni.navigateTo({
          url: '../../pages/DoWork/DoWork'
        })
      }
    }
  }
</script>

<style>

</style>
