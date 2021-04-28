<template>
  <view>
    <wechat-data></wechat-data>
    <view class="student">
      <text>家长信息</text>
      <view>
        <view class="parent">
          <text>关系：母子</text><br>
          <text>家长姓名</text>
          <text>家长手机号</text>
        </view>
        <view class="parent"><u-button>绑定家长</u-button></view>
      </view>
    </view>
    <u-button @click="toMessage">消息中心 要显示消息数量吗</u-button>
    <u-button>设置</u-button>
    <u-button>更新日志 这个需要用到吗</u-button>
    <u-button>版本信息？</u-button>
    <u-button>帮助文档 一个页面？</u-button>
    <u-button>投诉建议 一个页面？</u-button>
    <u-button>清理缓存</u-button>
    <stu-tabbar :selectedWhich=1></stu-tabbar>
  </view>
</template>

<script>
import WechatData from '../../components/WechatData/WechatData.vue'
import StuTabbar from '../../components/StuTabbar/StuTabbar.vue'
export default {
  data () {
    return {
    }
  },
  components: {
    WechatData,
    StuTabbar
  },
  methods: {
    toMessage () {
      this.$u.route({
        url: 'pages/Message/Message'
      })
    }
  }
}
</script>

<style scoped>
  .addclass {
    display: inline-block;
  }

  .parent {
    display: inline-block
  }
</style>
