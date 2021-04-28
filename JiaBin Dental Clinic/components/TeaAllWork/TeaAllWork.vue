<template>
  <view>
    <view>
      <u-button @click="newWork">发布作业</u-button>
      <u-cell-group title-bg-color="rgb(243, 244, 246)" :title="item.groupName" v-for="(item, index) in list" :key="index">
        <u-cell-item :titleStyle="{fontWeight: 500}" @click="openPage(item1.path)" v-for="(item1, index1) in item.list"
          :key="index1">
          <tea-work></tea-work>
        </u-cell-item>
      </u-cell-group>
    </view>
  </view>
</template>

<script>
import TeaWork from '../../components/TeaWork/TeaWork.vue'
export default {
  data() {
    return {
      list: [{
        groupName: '已发布作业',
        list: [{
          path: '/pages/SingleWorkAllStudent/SingleWorkAllStudent',
          icon: 'form',
          title: '小刘'
        }, {
          path: '/pages/SingleWorkAllStudent/SingleWorkAllStudent',
          icon: 'form',
          title: '小李'
        }, {
          path: '/pages/SingleWorkAllStudent/SingleWorkAllStudent',
          icon: 'form',
          title: 's2'
        }, {
          path: '/pages/SingleWorkAllStudent/SingleWorkAllStudent',
          icon: 'form',
          title: 's2'
        }]
      }]
    }
  },
  components: {
    TeaWork
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
