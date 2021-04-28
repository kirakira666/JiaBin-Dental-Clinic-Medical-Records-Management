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
              <u-radio-group :size="size" :width="width" :wrap="wrap" v-model="value" :activeColor="activeColor"
                :disabled="disabled">
                <view v-for="(item, index) in list">
                  <u-radio @change="radioChange(index)" :key="index" :name="item.option" :shape="shape" :disabled="item.disabled">{{item.content}}</u-radio>
                </view>
              </u-radio-group>
            </view>
          </u-card>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        list: [{
            content: '正确',
            checked: false,
            disabled: false
          },
          {
            content: '错误',
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
        type: '判断题',
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
    props: ["disabled"],
    methods: {
      radioChange(index) {
        this.answer = this.list[index].content
        console.log(index);
      },
    }
  }
</script>

<style scoped lang="scss">
  video {
    width: 100%;
  }
</style>
