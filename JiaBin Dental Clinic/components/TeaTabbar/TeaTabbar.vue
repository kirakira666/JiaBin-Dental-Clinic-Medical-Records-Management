<template>
  <view class="tea-tabbar">
    <view class="each-tab" v-for="(item, index) in tablist" :key=index @tap="change(index)">
      <view class="tab-image">
        <image class="image" v-if="index === selectedWhich" :src="item.selectedIconPath"></image>
        <image class="image" v-else :src="item.iconPath"></image>
      </view>
      <view :class="index === selectedWhich ? 'selected-tab-text' : 'tab-text'">
        {{item.text}}
      </view>
    </view>
  </view>
</template>

<script>
export default {
  props: {
    selectedWhich: {
      type: Number,
      default: 0
    }
  },
  data () {
    return {
      tablist: [{
        pagePath: '../../pages/CourseList/CourseList',
        text: '班级列表',
        iconPath: '../../static/course.png',
        selectedIconPath: '../../static/selected-course.png'
      },
      {
        pagePath: '../../pages/Center/Center',
        text: '个人中心',
        iconPath: '../../static/center.png',
        selectedIconPath: '../../static/selected-center.png'
      }
      ]
    }
  },
  methods: {
    change (index) {
      // this.selectedWhich = index
      // console.log('click!')
      // console.log(index === this.selectedWhich)
      if (this.selectedWhich !== index) {
        uni.redirectTo({
          url: this.tablist[index].pagePath
        })
      }
      // this.$emit('changePage',index)
    }
  }
}
</script>

<style scoped>
  .tea-tabbar {
    position: fixed;
    width: 100%;
    border: solid 1rpx #2C405A;
    bottom: var(--window-bottom);
    height: 140rpx;
    z-index: 999;
    background-color: white;
  }

  .each-tab {
    width: 50%;
    text-align: center;
    display: inline-block;
  }

  .tab-text {
    color: #000000;
  }

  .selected-tab-text {
    color: #18B566;
  }

  .image {
    width: 50rpx;
    height: 50rpx;
  }
</style>
