<template>
  <view>
    <u-subsection :current=Inv :list="['普通作业', '考试','相册']" @change="modeChange"></u-subsection>
    <u-upload ref="uUpload" max-count="6" @on-uploaded="onUploaded" @on-remove="onRemove" :action="action" :file-list="fileList"></u-upload>
    <image src="" mode=""></image>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        action: 'http://www.example.com/upload',
        fileList: [

        ],
        fileArr: [],
        Inv: 2,
        path: [
          '/pages/CommonWork/CommonWork',
          '/pages/StuTest/StuTest',
          '/pages/ClassPhoto/ClassPhoto'
        ]
      }
    },
    methods: {
      onUploaded(lists) {
        this.filesArr = lists;
      },
      onRemove(index, lists) {
        console.log('图片已被移除')
      },
      modeChange (index) {
        this.Inv = index
        uni.redirectTo({
          url: this.path[index]
        })
      }
    }
  }
</script>

<style>

</style>
