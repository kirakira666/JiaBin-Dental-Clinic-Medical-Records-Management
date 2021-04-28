<template>
  <view>
    <view>
      <class-work-info></class-work-info>
      <u-cell-group title-bg-color="rgb(243, 244, 246)" :title="item.groupName" v-for="(item, index) in list" :key="index">
        <u-cell-item :titleStyle="{fontWeight: 500}" @click="openPage(item1.path)" v-for="(item1, index1) in item.list"
          :key="index1">
          <stu-work-info></stu-work-info>
        </u-cell-item>
      </u-cell-group>
    </view>
  </view>
</template>

<script>
import ClassWorkInfo from '../../components/ClassWorkInfo/ClassWorkInfo'
import StuWorkInfo from '../../components/StuWorkInfo/StuWorkInfo'
export default {
  data() {
    return {
      list: [{
        groupName: '学生列表：',
        list: [{
          path: '/pages/TeaStuSingleWork/TeaStuSingleWork',
          icon: 'form',
          title: '小刘'
        }, {
          path: '/pages/TeaStuSingleWork/TeaStuSingleWork',
          icon: 'form',
          title: '小李'
        }, {
          path: '/pages/TeaStuSingleWork/TeaStuSingleWork',
          icon: 'form',
          title: 's2'
        }, {
          path: '/pages/TeaStuSingleWork/TeaStuSingleWork',
          icon: 'form',
          title: 's2'
        }]
      }]
    }
  },
  components: {
    ClassWorkInfo,
    StuWorkInfo
  },
  methods: {
    newWork () {
      this.$u.route({
        url: 'pages/NewWork/NewWork'
      })
    },
    openPage (path) {
      this.$u.route({
        url: path
      })
    }
  }
}
</script>

<style>

</style>
