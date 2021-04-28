<template>
  <view>
    <view class="u-demo-wrap">
      <view class="u-demo-area">
        <view class="">
          <u-card :title="number" :sub-title="type" :padding="padding" :border="border">
            <view class="" slot="body">
              <view class="u-body-item u-flex u-border-bottom u-col-between u-p-t-0">
                <view class="u-body-item-title">
                  {{title.content}}
                </view>
              </view>
              <view class="u-body-item u-flex u-row-between u-p-b-0">
                <video :src="title.link" v-if="title.linktype=='video'"></video>
                <image :src="title.link" v-else-if="title.linktype=='image'"></image>
                <audio :src="title.link" v-else-if="title.linktype=='audio'"></audio>
              </view>
              <u-radio-group :size="size" :width="width" :wrap="wrap" v-model="value" :activeColor="activeColor">
                <view v-for="(item, index) in list">
                  <u-radio @change="radioChange(index)" :key="index" :name="item.option" :shape="shape" :disabled="true">{{item.option}}.</u-radio>
                  <view v-if="item.type=='text'">{{item.content}}</view>
                  <video v-else-if="item.type=='video'" :src="item.content"></video>
                  <audio v-else-if="item.type=='audio'" :src="item.content"></audio>
                  <image v-else-if="item.type=='image'" :src="item.content"></image>
                </view>
              </u-radio-group>
            </view>
          </u-card>
          <view class="wrap">
            <view>
              学生答案：{{stuAnswer}}
            </view>
            <view>
              参考答案：{{realAnswer}}
            </view>
            <u-form :model="model" ref="uForm">
              <u-form-item label-position="right" label="点评:" prop="comment">
                <u-input type="textarea" placeholder="添加点评" v-model="model.comment" />
              </u-form-item>
            </u-form>
            <u-button size="medium" @click="submit">提交点评</u-button>
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
      </view>
    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        model: {
          comment: ''
        },
        list: [{
            option: 'A',
            content: '荔枝',
            type: 'text',
            checked: false,
            disabled: false
          },
          {
            option: 'B',
            content: '香蕉',
            type: 'image',
            checked: false,
            disabled: false
          },
          {
            option: 'C',
            content: '橙子',
            type: 'video',
            checked: false,
            disabled: false
          },
          {
            option: 'D',
            content: '草莓',
            type: 'audio',
            checked: false,
            disabled: false
          }
        ],
        disabled: false,
        shape: 'circle',
        value: '',
        answer: '',
        activeColor: '#2979ff',
        size: 34,
        wrap: false,
        width: '100%',
        number: '',
        type: '单选题',
        title: {
          content: '猜猜',
          link: '',
          linktype: '',
        },
        status: '',
        correctAnswer: '',
        analysis: '',
        remark: '',
        identity: '',
      };
    },
    mounted() {
      
    },
    props: {
      stuAnswer: String,
      realAnswer: String
    },
    methods: {
      radioChange(index) {
        this.answer = this.list[index].option
        console.log(index);
      },
      submit() {
        console.log(this.model.comment);
      }
    }
  }
</script>

<style scoped lang="scss">
  video {
    width: 100%;
  },
  .wrap {
    padding: 30rpx;
  }
</style>
