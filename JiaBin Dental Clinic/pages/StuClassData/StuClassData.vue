<template>
  <view>
    <u-subsection :current=Inv :list="['普通作业', '考试','相册']" @change="modeChange"></u-subsection>
    <view v-show="Inv === 0"><common-work></common-work></view>
    <view v-show="Inv === 1"><stu-test v-show="Inv === 1"></stu-test></view>
    <view v-show="Inv === 2"><class-photo v-show="Inv === 2"></class-photo></view>
  </view>
</template>

<script>
import CommonWork from '../../components/CommonWork/CommonWork.vue'
import StuTest from '../../components/StuTest/StuTest.vue'
import ClassPhoto from '../../components/ClassPhoto/ClassPhoto.vue'
export default {
  data () {
    return {
      Inv: 0
    }
  },
  components: {
    CommonWork,
    StuTest,
    ClassPhoto
  },
  methods: {
    modeChange (index) {
      this.Inv = index
    },
    changeTab (Inv) {
      that.navIdx = Inv
    }
  }
}
</script>

<style>

</style>
