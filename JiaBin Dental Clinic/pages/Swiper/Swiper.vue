<template>
  <view class="u-demo">
    <view class="u-demo-wrap">
      <view class="u-demo-area">
        <u-toast ref="uToast"></u-toast>
        <u-swiper :autoplay=false :height="1182" :list="list" :title="title" 
        :indicator-pos="indicatorPos" :interval="3000" @click="click"></u-swiper>
        <u-modal ref="uModal" v-model="show" :show-cancel-button="true"
        	:show-title="false" :async-close="true"
        	@confirm="confirm" :content="content"
          v-if="show">
        </u-modal>
        <u-modal ref="uModal" v-model="showPhone" :show-cancel-button="true"
        	:show-title="false" :async-close="true"
        	@confirm="confirmPhone" :content="contentPhone"
          v-if="show">
        </u-modal>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data () {
    return {
      list: [{
        image: 'https://cdn.uviewui.com/uview/swiper/1.jpg',
        title: '第一张图片标题'
      },
      {
        image: 'https://cdn.uviewui.com/uview/swiper/2.jpg',
        title: '第二张图片标题'
      },
      {
        image: 'https://cdn.uviewui.com/uview/swiper/3.jpg',
        title: '第三张图片标题'
      }
      ],
      title: true,//显不显示标题
      mode: 'round',
      indicatorPos: 'bottomCenter',
      effect3d: false,
      show: false,
      showPhone: false,
      userInfo: {},
      content: '申请获取您的头像和昵称',
      contentPhone: '申请获取您的电话号码',
      phone: '',
      openid: ''
    }
  },
  methods: {
    click(index) {
    	// this.$refs.uToast.show({
    	// 	title: `点击了第${index + 1}张图片`,
    	// 	type: 'success'
    	// })
      if (index === 2) {
        this.show = true
      }
    },
    confirmPhone() {  /*获取电话功能要在上线后才能完成*/
      let that = this
      wx.request({
        url:getApp().globalData.baseUrl + 'user/',
        method:'POST',
        header: {
          'content-type': 'application/json'
        },
        data: {
          // 'openid': that.openid,
          'openid': 'webdfzzdsffk',
          'nick': '啦啦啦',
          // 'phone': that.phone,
          'phone': '12345666601',
          'avatar': that.userInfo.avatarUrl,
          'gender': that.userInfo.gender
        },
        success() {
          uni.reLaunch({
            url: '/pages/ChooseIdentity/ChooseIdentity',
            animationType: 'slide-in-bottom'
          })
        },
        fail() {
          console.log('fail')
        }
      })
    },
    confirm() {
      let that = this
      wx.login({
        success(res) {
          if(res.code) {
            let code = res.code
              wx.getUserInfo({
                success:function(res) {
                  that.userInfo = res.userInfo
                  console.log(that.userInfo)
                  that.showPhone = true
                 },
                fail:res=>{
                  console.log('fail')
                }
              })
            }
          }
        })
    	setTimeout(() => {
    		this.show = false;
    	}, 2000)
    },
    // change (index) {
    //   if (index === 0) {
    //     console.log(index)
    //     // 在这里跳转页面
    //     uni.reLaunch({
    //       url: '/pages/ChooseIdentity/ChooseIdentity',
    //       animationType: 'slide-in-bottom'
    //     })
    //   }
    //   // console.log(index);
    // }
  }
}
</script>

<style lang="scss" scoped>
  .item {
    margin: 30rpx 0;
  }
</style>
