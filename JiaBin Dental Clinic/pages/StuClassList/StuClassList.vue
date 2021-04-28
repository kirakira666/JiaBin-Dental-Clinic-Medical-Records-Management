<template>
  <view>
    <view>
      <text class="addclass">我的班级列表</text>
      <u-button class="addclass" @click="toScan">加入班级</u-button>
    </view>
    <stu-class @toClass="perClass"></stu-class>
    <stu-tabbar :selectedWhich=0 @changePage="change"></stu-tabbar>
  </view>
</template>

<script>
import StuClass from '../../components/StuClass/StuClass.vue'
import StuTabbar from '../../components/StuTabbar/StuTabbar.vue'
export default {
  data () {
    return {
    }
  },
  components: {
    StuClass,
    StuTabbar
  },
  methods: {
    toScan () {
      uni.scanCode({
        success: function (res) {
          console.log('扫码成功')
          uni.showToast({
            title: '扫码成功！'
          })
        },
        fail: function (e) {
          console.log('扫码失败')
        }
      })
    },
    perClass () {
      console.log('click!')
      uni.navigateTo({
        url: '/pages/StuClassData/StuClassData'
      })
    }
  }
}
</script>

<style>
  .addclass {
    display: inline;
  }
</style>
