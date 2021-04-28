<template>
  <view class="u-demo">
    <view class="u-demo-wrap">
      <view class="u-demo-title">{{title}}</view>
    </view>
    <view class="u-config-wrap">
      <view class="u-config-item">
        <u-subsection vibrateShort current='1' :list="['班级', '题库']" @change="modeChange"></u-subsection>
      </view>
    </view>
    <view>
      <course-list></course-list>
    </view>
  </view>
</template>

<script>
import CourseList from '../../components/CourseList/CourseList.vue'
export default {
  data () {
    return {
      title: '题库',
      mode: 'circle',
      text: '', // 优先级比src高
      size: '90'
    }
  },
  components: {
    CourseList
  },
  computed: {
    getIcon () {
      return path => {
        return 'https://cdn.uviewui.com/uview/example/' + path + '.png'
      }
    }
  },
  methods: {
    modeChange (index) {
      console.log('hhhhhh')
      if (index === 0) {
        this.$u.route({
          url: '/pages/TeaClassList/TeaClassList'
        })
      } else if (index === 1) {
        this.$u.route({
          url: '/pages/QuestionBank/QuestionBank'
        })
      }
    }
  }
}
</script>

<style lang="scss" scoped>
  .u-cell-icon {
    height: 40rpx;
    width: 40rpx;
  }
</style>
