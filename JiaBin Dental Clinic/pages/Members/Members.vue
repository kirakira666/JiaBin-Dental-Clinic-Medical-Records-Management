<template>
  <view class="u-demo">
    <u-button>邀请学生进班</u-button>
    <u-button @click="toCode">查看班级二维码</u-button>
    <u-subsection :current=Inv :list="['成员', '统计', '作业', '相册']" @change="modeChange"></u-subsection>
    <view class="" v-show="Inv == 0">
      <!-- 班级成员Members -->
      <u-cell-group title-bg-color="rgb(243, 244, 246)" :title="item.groupName" v-for="(item, index) in list" :key="index">
        <u-cell-item :titleStyle="{fontWeight: 500}" @click="openPage(item1.path)" :title="item1.title" v-for="(item1, index1) in item.list"
          :key="index1">
          <image slot="icon" class="u-cell-icon" :src="getIcon(item1.icon)" mode="widthFix"></image>
        </u-cell-item>
      </u-cell-group>
    </view>
    <view class="" v-show="Inv == 1">
      <!-- 班级作业统计DataCount -->
      <u-cell-group title-bg-color="rgb(243, 244, 246)" :title="item.groupName" v-for="(item, index) in list2" :key="index">
        <u-cell-item :titleStyle="{fontWeight: 500}" @click="openPage(item2.path)" v-for="(item2, index2) in item.list2"
          :key="index2">
          <work-data></work-data>
        </u-cell-item>
      </u-cell-group>
    </view>
    <view class="" v-show="Inv == 2">
      <!-- 作业CommonWork -->
      <text>未提交</text>
      <stu-work></stu-work>
      <text>已提交</text>
      <stu-work></stu-work>
    </view>
    <view class="" v-show="Inv == 3">
      <!-- 相册ClassPhoto -->
      <view>
        <u-upload ref="uUpload" max-count="6" @on-uploaded="onUploaded" @on-remove="onRemove" :action="action"
          :file-list="fileList"></u-upload>
        <image src="" mode=""></image>
      </view>
    </view>

  </view>
</template>

<script>
import WorkData from '../../components/WorkData/WorkData.vue'
import StuWork from '../../components/StuWork/StuWork.vue'
export default {
  data () {
    return {
      action: 'http://www.example.com/upload',
      fileList: [
      ],
      fileArr: [],
      Inv: 0,
      title: '班级成员',
      mode: 'circle',
      text: '', // 优先级比src高
      size: '90',
      list: [{
        groupName: '老师',
        list: [{
          path: '/pages/TeaClassList/TeaClassList',
          icon: 'tag',
          title: '刘老师'
        }, {
          path: '/pages/TeaClassList/TeaClassList',
          icon: 'tag',
          title: '李老师'
        }]
      },
      {
        groupName: '学生',
        list: [{
          path: '/pages/TeaClassList/TeaClassList',
          icon: 'form',
          title: 's1'
        }, {
          path: '/pages/TeaClassList/TeaClassList',
          icon: 'form',
          title: 's2'
        }]
      }
      ],
      list2: [{
        groupName: '作业提交情况',
        list2: [{
          path: '/pages/TeaClassList/TeaClassList',
          icon: 'form',
          title: '小刘'
        }, {
          path: '/pages/TeaClassList/TeaClassList',
          icon: 'form',
          title: '小李'
        }, {
          path: '/pages/TeaClassList/TeaClassList',
          icon: 'form',
          title: 's2'
        }, {
          path: '/pages/TeaClassList/TeaClassList',
          icon: 'form',
          title: 's2'
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
    WorkData,
    StuWork
  },
  methods: {
    onUploaded (lists) {
      this.filesArr = lists
    },
    onRemove (index, lists) {
      console.log('图片已被移除')
    },
    changeTab (Inv) {
      that.navIdx = Inv
    },
    modeChange (index) {
      this.Inv = index
    },
    openPage (path) {
      this.$u.route({
        url: path
      })
    },
    toCode () {
      this.$u.route({
        url: 'pages/Code/Code'
      })
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
