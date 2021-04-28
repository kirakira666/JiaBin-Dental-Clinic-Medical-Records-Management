<template>
  <view class="u-demo">
    <view class="">
      <u-cell-group title-bg-color="rgb(243, 244, 246)" :title="item.groupName" v-for="(item, index) in list" :key="index">
        <u-cell-item :titleStyle="{fontWeight: 500}" @click="openPage(item1.path)" :title="item1.title" v-for="(item1, index1) in item.list"
          :key="index1">
          <image slot="icon" class="u-cell-icon" :src="getIcon(item1.icon)" mode="widthFix"></image>
        </u-cell-item>
      </u-cell-group>
    </view>
    <tea-tabbar :selectedWhich=0></tea-tabbar>
  </view>
</template>

<script>
import TeaTabbar from '../../components/TeaTabbar/TeaTabbar.vue'
export default {
  data () {
    return {
      title: '课程首页',
      mode: 'circle',
      text: '', // 优先级比src高
      size: '90',
      list: [{
        groupName: '课程列表',
        list: [{
          path: '/pages/TeaClassList/TeaClassList',
          icon: 'form',
          title: '课程一'
        }, {
          path: '/pages/TeaClassList/TeaClassList',
          icon: 'form',
          title: '课程一'
        }]
      }
      ]
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
    TeaTabbar
  },
  methods: {
    changeTab (Inv) {
      that.navIdx = Inv
    },
    openPage (path) {
      this.$u.route({
        url: path
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

  .addclass {
    display: inline-block;
  }

  .parent {
    display: inline-block
  }
</style>
