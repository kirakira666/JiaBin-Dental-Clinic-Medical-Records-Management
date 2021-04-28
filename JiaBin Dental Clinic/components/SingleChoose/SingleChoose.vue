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
                  <u-radio @change="radioChange(index)" :key="index" :name="item.option" :shape="shape" :disabled="item.disabled">{{item.option}}.</u-radio>
                  <view v-if="item.type=='text'">{{item.content}}</view>
                  <video v-else-if="item.type=='video'" :src="item.content"></video>
                  <audio v-else-if="item.type=='audio'" :src="item.content"></audio>
                  <image v-else-if="item.type=='image'" :src="item.content"></image>
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
    props: ["disabled"],
    methods: {
      radioChange(index) {
        this.answer = this.list[index].option
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
