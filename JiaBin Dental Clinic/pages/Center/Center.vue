<template>
  <view>
    <wechat-data></wechat-data>
    <view class="teacher">
      <view class="addclass">
        <text>班级数量10个</text><br>
        <text>已开3个班</text>
        <text>还可以开7个班</text>
      </view>
      <view class="addclass">
        <u-button>增加班容（老师用）</u-button>
      </view>
    </view>
    <u-button @click="toMessage">消息中心 要显示消息数量吗</u-button>
    <u-button>设置</u-button>
    <u-button>更新日志 这个需要用到吗</u-button>
    <u-button>版本信息？</u-button>
    <u-button>帮助文档 一个页面？</u-button>
    <u-button>投诉建议 一个页面？</u-button>
    <u-button>清理缓存</u-button>
    <tea-tabbar :selectedWhich=1></tea-tabbar>
  </view>
</template>

<script>
import WechatData from '../../components/WechatData/WechatData.vue'
import TeaTabbar from '../../components/TeaTabbar/TeaTabbar.vue'
export default {
  data () {
    return {

    }
  },
  components: {
    WechatData,
    TeaTabbar
  },
  methods: {
    toMessage () {
      console.log("message")
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
