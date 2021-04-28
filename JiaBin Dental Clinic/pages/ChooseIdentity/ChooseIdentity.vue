<template>
  <view>
    <view>
      <text>请选择身份进入小程序</text>
    </view>
    <view>
      <u-button @click="toTeacher">老师</u-button>
    </view>
    <view>
      <u-button @click="toStudent">学生</u-button>
    </view>
    <view>
      <u-button @click="toParent">家长</u-button>
    </view>
    <block v-if="inputName">
      <view class='toast-box'>        
        <view class='toastbg'></view>        
        <view class='showToast'>            
          <view class='toast-title'>                
            <text>您还未创建该身份，请输入姓名创建身份</text>            
          </view>            
          <view class='toast-main'>                
            <view class='toast-input'>                    
              <input type='text' placeholder='输入姓名' v-model="name"></input>                
            </view>            
          </view>            
          <view class='toast-button'>                
            <view class='button1'>                    
              <button @click='cancel'>取消</button>                
            </view>                
            <view class='button2'>                    
              <button @click='confirm'>确定</button>                
            </view>            
          </view>        
        </view>    
      </view>
    </block>
  </view>
</template>

<script>
export default {
  data () {
    return {
      inputName: false,
      name: ''
    }
  },
  methods: {
    toTeacher () {
      getApp().globalData.identity_type = 1
      let that = this
      wx.request({
        url:getApp().globalData.baseUrl + 'choose/' + getApp().globalData.user_id + '/1',
        method:'GET',
        header: {
          'content-type': 'application/json'
        },
        success(res) {
          if (res.data !== 0) {
            getApp().globalData.identity_id = res.data
            that.$u.route({
              url: '/pages/TeaClassList/TeaClassList',
              animationType: 'slide-in-bottom'
            })
          } else {
            that.inputName = true
          }
        },
        fail() {
          console.log('fail')
        }
      })
    },
    toStudent () {
      getApp().globalData.identity_type = 2
      let that = this
      wx.request({
        url:getApp().globalData.baseUrl + 'choose/' + getApp().globalData.user_id + '/2',
        method:'GET',
        header: {
          'content-type': 'application/json'
        },
        success(res) {
          if (res.data !== 0) {
            getApp().globalData.identity_id = res.data
            that.$u.route({
              url: '/pages/StuClassList/StuClassList',
              animationType: 'slide-in-bottom'
            })
          } else {
            that.inputName = true
          }
        },
        fail() {
          console.log('fail')
        }
      })
    },
    toParent () {
      getApp().globalData.identity_type = 3
      let that = this
      wx.request({
        url:getApp().globalData.baseUrl + 'choose/' + getApp().globalData.user_id + '/3',
        method:'GET',
        header: {
          'content-type': 'application/json'
        },
        success(res) {
          if (res.data !== 0) {
            getApp().globalData.identity_id = res.data
            that.$u.route({
              url: '/pages/StuClassList/StuClassList',
              animationType: 'slide-in-bottom'
            })
          } else {
            that.inputName = true
          }
        },
        fail() {
          console.log('fail')
        }
      })
    },
    cancel () {
      this.inputName = false
    },
    confirm () {
      let that = this
      let type = getApp().globalData.identity_type
      let user = ['teacher', 'student', 'parent']
      wx.request({
        url:getApp().globalData.baseUrl + user[type - 1] + '/',
        method:'POST',
        header: {
          'content-type': 'application/json'
        },
        data: {
          user_id: getApp().globalData.user_id,
          name: that.name
        },
        success(res) {
          console.log(res)
          getApp().globalData.identity_id = res.data.id
          if (type === 1) {
            that.$u.route({
              url: '/pages/TeaClassList/TeaClassList',
              animationType: 'slide-in-bottom'
            })
          } else {
            that.$u.route({
              url: '/pages/StuClassList/StuClassList',
              animationType: 'slide-in-bottom'
            })
          }
        },
        fail() {
          console.log('fail')
        }
      })
    }
  }
}
</script>

<style>
.toast-box {    
  width: 100%;    
  height: 100%;    
  opacity: 1;    
  position: fixed;    
  top: 0px;    
  left: 0px;
}  
.toastbg {    
  opacity: 0.2;    
  background-color: black;    
  position: absolute;    
  width: 100%;    
  min-height: 100vh;
} 
.showToast {    
  position: absolute;    
  opacity: 1;    
  width: 70%;    
  margin-left: 15%;    
  margin-top: 40%;
} 
.toast-title {    
  padding-left: 5%;    
  background-color: white;    
  color: black;    
  padding-top: 2vh;    
  padding-bottom: 2vh;    
  border-top-right-radius: 16rpx;    
  border-top-left-radius: 16rpx;
} 

.toast-main {    
  padding-top: 2vh;    
  padding-bottom: 2vh;    
  background-color: white;    
  text-align: center;
} 

.toast-input {    
  margin-left: 5%;    
  margin-right: 5%;    
  border: 1px solid #ddd;    
  padding-left: 2vh;    
  padding-right: 2vh;    
  padding-top: 1vh;    
  padding-bottom: 1vh;
} 
.toast-button {    
  display: flex;
} 
.button1 {    
  width: 50%;
} 
.button2 {    
  width: 50%;
} 
.button1 button {    
  width: 100%;    
  background-color: white;    
  color: gray;    
  border-radius: 0px;    
  border-bottom-left-radius: 16rpx;
} 
.button2 button{    
  width: 100%;    
  background-color: white;    
  color: black;    
  border-radius: 0px;    
  border-bottom-right-radius: 16rpx;
}

</style>
