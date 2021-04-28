<template>
  <view>
    <view>
      <view v-show="current !== 0" class="menu">
        <u-button type="default" @click="last">上一题</u-button>
      </view>
      <view class="menu">
        <u-button type="default">快速跳转</u-button>
      </view>
      <view v-show="current !== (length - 1)" class="menu" >
        <u-button type="default" @click="next">下一题</u-button>
      </view>
    </view>
    <view>
      当前题目序号：{{current + 1}}
      {{ problemList[current].type}}
    </view>
    <view v-show="problemList[current].type === '单项选择'">
      <single-choose></single-choose>
    </view>
    <view v-show="problemList[current].type === '多项选择'">
      <multi-choose></multi-choose>
    </view>
    <view v-show="problemList[current].type === '判断题'">
      <true-or-false></true-or-false>
    </view>
    <view v-show="current === (length - 1)">
      <u-button @click="submit">提交</u-button>
    </view>
  </view>
</template>

<script>
  import SingleChoose from '../../components/SingleChoose/SingleChoose.vue'
  import MultiChoose from '../../components/MultiChoose/MultiChoose.vue'
  import TrueOrFalse from '../../components/TrueOrFalse/TrueOrFalse.vue'
  export default {
    data() {
      return {
        current: 0,
        length: 3,
        count: 0,
        // 已完成的题目数量
        problemList: [{
            type: '单项选择'
          },
          {
            type: '多项选择'
          },
          {
            type: '判断题'
          }
        ]
      }
    },
    components: {
      SingleChoose,
      MultiChoose,
      TrueOrFalse
    },
    methods: {
      last() {
        this.current--
      },
      next() {
        this.current++
      },
      submit () {
        if (this.count !== this.length) {
          uni.showModal({
            title: '题目未全部完成',
            content: '您还没有完成全部题目，请全部完成再点击提交！',
          })
        } else {
          console.log('提交答案')
        }
      }
    }
  }
</script>

<style>
  .menu {
    display: inline-block;
    margin-left: 20rpx
  }
</style>
