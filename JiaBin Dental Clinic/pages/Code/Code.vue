<template>
  <view class="code">
    <view class="qrimg">
      <tki-qrcode
        ref="qrcode"
        :cid="cid"
        :val="val"
        :size="size"
        :background="background"
        :foreground="foreground"
        :pdground="pdground"
        :icon="icon"
        :iconSize="iconsize"
        :lv="lv" 
        :onval="onval"
        :loadMake="loadMake"
        :showLoading="showLoading"
        :loadingText="loadingText"
        @result="code" />
    </view>
    <view>
      扫码加入班级
    </view>
  </view>
</template>

<script>
import tkiQrcode from "@/components/tki-qrcode/tki-qrcode.vue"

export default {
  data () {
    return {
      cid: 'tki-qrcode-canvas',
      val: 'www.baidu.com',
      size: 200,
      background: '#ffffff',
      foreground: '#000000',
      pdground: '#000000',
      icon: '../../static/selected-class.png',
      iconsize: 45,
      lv: 3,
      onval: true,
      loadMake: true,
      src: '../../static/',
      showLoading: true,
      loadingText: '加载中，请稍候',
      
    }
  },
  components: {
    tkiQrcode
  },
  methods: {
    code (path) {
      console.log(path)
    }
  },
}
</script>

<style>
  .code {
    text-align: center;
    margin: auto;
    margin-top: 200rpx;
  }
</style>
