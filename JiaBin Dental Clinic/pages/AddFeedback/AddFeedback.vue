<template>
  <view>
    <view>
      <quick-redirect :btnList="problemList" @onFather="Father"></quick-redirect>
      <view v-show="current !== 0" class="menu">
        <u-button type="default" @click="last">上一题</u-button>
      </view>
      <view v-show="current !== (length - 1)" class="menu">
        <u-button type="default" @click="next">下一题</u-button>
      </view>
    </view>
    <view>
      当前题目序号：{{current + 1}}
      {{ problemList[current].type}}
    </view>
    <view v-show="problemList[current].type === '单项选择'">
      <single-choose :disabled="true"></single-choose>
    </view>
    <view v-show="problemList[current].type === '多项选择'">
      <multi-choose :disabled="true"></multi-choose>
    </view>
    <view v-show="problemList[current].type === '判断题'">
      <true-or-false :disabled="true"></true-or-false>
    </view>
    <view v-show="current === (length - 1)">
      <u-button @click="submit">提交</u-button>
    </view>
    <view class="wrap">
      <view>
        学生答案：{{problemList[current].stuAnswer}}
      </view>
      <view>
        参考答案：{{problemList[current].realAnswer}}
      </view>
      <u-form :model="model" ref="uForm">
        <u-form-item label-position="right" label="点评:" prop="comment">
          <u-input type="textarea" placeholder="添加点评" v-model="model.comment" />
        </u-form-item>
      </u-form>
      <u-button size="medium" @click="comment">提交点评</u-button>
      <u-button size="medium" @click="like">点赞</u-button>
    </view>
    <view class="wrap">
      <u-card  title="解析：">
        <view class="" slot="body">
          <view>
            这是解析
          </view>
          <view>
            <video></video>
          </view>
        </view>
      </u-card>
    </view>
  </view>
</template>

<script>
  import SingleChoose from '../../components/SingleChoose/SingleChoose'
  import MultiChoose from '../../components/MultiChoose/MultiChoose.vue'
  import TrueOrFalse from '../../components/TrueOrFalse/TrueOrFalse'
  import QuickRedirect from '../../components/QuickRedirect/QuickRedirect'
  export default {
    data() {
      return {
        current: 0,
        length: 7,
        count: 0,
        model: {
          comment: ''
        },
        // 已完成的题目数量
        problemList: [{
            index: 1,
            type: '单项选择',
            stuAnswer: 'D',
            realAnswer: 'A'
          },
          {
            index: 2,
            type: '多项选择',
            stuAnswer: 'AD',
            realAnswer: 'ABD'
          },
          {
            index: 3,
            type: '判断题',
            stuAnswer: '正确',
            realAnswer: '错误'
          },
          {
            index: 4,
            type: '判断题',
            stuAnswer: '正确',
            realAnswer: '错误'
          },
          {
            index: 5,
            type: '判断题',
            stuAnswer: '正确',
            realAnswer: '错误'
          },
          {
            index: 6,
            type: '单项选择',
            stuAnswer: 'D',
            realAnswer: 'A'
          },
          {
            index: 7,
            type: '多项选择',
            stuAnswer: 'AD',
            realAnswer: 'ABD'
          }
        ]
      }
    },
    components: {
      SingleChoose,
      MultiChoose,
      TrueOrFalse,
      QuickRedirect
    },
    methods: {
      Father(e) {
        console.log(e)
        this.model.comment = ''
        this.current = e - 1
      },
      last() {
        this.current--
        this.model.comment = ''
      },
      next() {
        this.current++
        this.model.comment = ''
      },
      comment() {
        console.log(this.model.comment)
      },
      submit() {
        console.log(this.count)
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
