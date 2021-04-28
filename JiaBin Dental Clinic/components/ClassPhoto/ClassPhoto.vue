<template>
  <view>
    <u-upload ref="uUpload" max-count="6" @on-uploaded="onUploaded" @on-remove="onRemove" :action="action" :file-list="fileList"></u-upload>
    <image src="" mode=""></image>
  </view>
</template>

<script>
  export default {
    data () {
      return {
        action: 'http://10.130.209.129:8001/',
        fileList: [
        ],
        fileArr: [],
      }
    },
    methods: {
      onUploaded(lists) {
        this.filesArr = lists;
      },
      onRemove(index, lists) {
        console.log('图片已被移除')
      }
    }
}
</script>

<style>

</style>
