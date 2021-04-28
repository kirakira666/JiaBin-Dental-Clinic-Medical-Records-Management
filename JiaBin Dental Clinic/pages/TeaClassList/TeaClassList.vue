<template>
  <view>
    <u-subsection :current=Inv :list="['班级', '题库']" @change="modeChange"></u-subsection>
    <view class="" v-show="Inv == 0">
      <!-- 班级TeaClassList -->
      <u-button type="default" @click="newClass">新建班级</u-button>
      <u-button type="default" @click="scan">加入班级</u-button>
      <u-cell-group title-bg-color="rgb(243, 244, 246)" :title="item.groupName" v-for="(item, index) in list" :key="index">
        <u-cell-item :titleStyle="{fontWeight: 500}" @click="openPage(item1.path)" :title="item1.title" v-for="(item1, index1) in item.list"
          :key="index1">
          <image slot="icon" class="u-cell-icon" :src="getIcon(item1.icon)" mode="widthFix"></image>
        </u-cell-item>
      </u-cell-group>
    </view>
    <view class="" v-show="Inv == 1">
      <!-- 题库QuestionBank -->
      <view>
        <course-list></course-list>
      </view>
    </view>
  </view>
</template>

<script>
import CourseList from '../../components/CourseList/CourseList.vue'
export default {
  data () {
    return {
      Inv: 0,
      list: [{
        groupName: '班级：（icon是瞎加的）',
        list: [{
          path: '/pages/TeaClassData/TeaClassData',
          icon: 'form',
          title: '班级二'
        }, {
          path: '/pages/TeaClassData/TeaClassData',
          icon: 'form',
          title: '班级三'
        }]
      }]
    }
  },
  computed: {
    getIcon () {
      return path => {
        return 'https://cdn.uviewui.com/uview/example/' + path + '.png'
      }
    }
  },
  components: {
    CourseList
  },
  methods: {
    changeTab (Inv) {
      that.navIdx = Inv
    },
    openPage (path) {
      this.$u.route({
        url: path
      })
    },
    newClass () {
      uni.redirectTo({
        url: '/pages/NewClass/NewClass'
      })
    },
    modeChange (index) {
      this.Inv = index
    },
    scan () {
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
    }
  }
}
</script>

<style>
  .u-cell-icon {
    height: 40rpx;
    width: 40rpx;
  }
</style>
