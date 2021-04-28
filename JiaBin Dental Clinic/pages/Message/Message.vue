<template>
  <view>
    <u-subsection :current=Inv :list="['系统消息', '作业消息']" @change="modeChange"></u-subsection>
    <view class="" v-show="Inv == 0">
      <!-- 班级TeaClassList -->
      <u-cell-group title-bg-color="rgb(243, 244, 246)" :title="item.groupName" v-for="(item, index) in list" :key="index">
        <u-cell-item :titleStyle="{fontWeight: 500}" @click="openPage(item1.path)" v-for="(item1, index1) in item.list"
          :key="index1">
          <info-detail></info-detail>
        </u-cell-item>
      </u-cell-group>
    </view>
    <view class="" v-show="Inv == 1">
      <!-- 题库QuestionBank -->
      <view>
        <u-cell-group title-bg-color="rgb(243, 244, 246)" :title="item.groupName" v-for="(item, index) in list2" :key="index">
          <u-cell-item :titleStyle="{fontWeight: 500}" @click="openPage(item1.path)" v-for="(item1, index1) in item.list"
            :key="index1">
            <info-detail></info-detail>
          </u-cell-item>
        </u-cell-group>
      </view>
    </view>
  </view>
</template>

<script>
import CourseList from '../../components/CourseList/CourseList.vue'
import InfoDetail from '../../components/InfoDetail/InfoDetail.vue'
export default {
  data () {
    return {
      Inv: 0,
      list: [{
        groupName: '未读消息',
        list: [{
          path: '/pages/TeaClassData/TeaClassData',
          icon: 'form',
          title: '消息1'
        }, {
          path: '/pages/TeaClassData/TeaClassData',
          icon: 'form',
          title: '消息2'
        }]
      },{
        groupName: '已读消息',
        list: [{
          path: '/pages/TeaClassData/TeaClassData',
          icon: 'form',
          title: '班级二'
        }, {
          path: '/pages/TeaClassData/TeaClassData',
          icon: 'form',
          title: '班级三'
        }]
      }],
      list2: [{
        groupName: '未读消息',
        list: [{
          path: '/pages/TeaClassData/TeaClassData',
          icon: 'form',
          title: '消息1'
        }]
      },{
        groupName: '已读消息',
        list: [{
          path: '/pages/TeaClassData/TeaClassData',
          icon: 'form',
          title: '班级二'
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
    CourseList,
    InfoDetail
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
