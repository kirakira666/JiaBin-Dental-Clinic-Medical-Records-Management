<template>
  <view class="">
    <wechat-data></wechat-data>
    <view class="wrap">
      <u-form :model="model" :rules="rules" ref="uForm" :errorType="errorType">
        <u-form-item label-width="700" label="请输入班级码:">
        </u-form-item>
        <u-form-item label-width="120" :label-position="labelPosition" label="班级码" prop="classCode">
          <u-input :border="border" placeholder="请输入班级码" v-model="model.classCode" type="text"></u-input>
        </u-form-item>
      </u-form>
      <view class="agreement">
        <u-checkbox v-model="check" @change="checkboxChange"></u-checkbox>
        <view class="agreement-text">
          勾选代表同意我们的班级码激活协议
        </view>
      </view>
      <u-button @click="submit">验证</u-button>
      <u-select mode="mutil-column-auto" :list="selectList" v-model="selectShow" @confirm="selectConfirm"></u-select>
    </view>
  </view>
</template>

<script>
import WechatData from '../../components/WechatData/WechatData'
export default {
  data () {
    let that = this
    return {
      model: {
        name: '',
        classType: '封闭式',
        courseType: '',
        classCode: '',
        agreement: false
      },
      rules: {
        classCode: [{
            required: true,
            message: '请输入班级码',
            trigger: 'blur'
          },
          {
            min: 8,
            max: 8,
            message: '不合法班级码！班级码由8位数字或字符组成！',
            trigger: ['change', 'blur']
          },
          // 异步验证，用途：比如用户注册时输入完账号，后端检查账号是否已存在
          // {
          // 	trigger: ['blur'],
          // 	// 异步验证需要通过调用callback()，并且在里面抛出new Error()
          // 	// 抛出的内容为需要提示的信息，和其他方式的message属性的提示一样
          // 	asyncValidator: (rule, value, callback) => {
          // 		this.$u.post('/ebapi/public_api/index').then(res => {
          // 			// 如果验证出错，需要在callback()抛出new Error('错误提示信息')
          // 			if(res.error) {
          // 				callback(new Error('姓名重复'));
          // 			} else {
          // 				// 如果没有错误，也要执行callback()回调
          // 				callback();
          // 			}
          // 		})
          // 	},
          // }
        ],
      },
      border: false,
      check: false,
      codeAvailable: false,
      selectStatus: 'close',
      labelPosition: 'left',
      codeTips: '',
      errorType: ['message']
    }
  },
  components: {
    WechatData
  },
  onLoad (option) {
    this.model.name = option.name
    this.model.courseType = option.courseType
  },
  computed: {
    borderCurrent () {
      return this.border ? 0 : 1;
    }
  },
  onReady () {
    this.$refs.uForm.setRules(this.rules)
  },
  methods: {
    submit () {
      this.$refs.uForm.validate(valid => {
        if (valid) {
          if (!this.model.agreement) return this.$u.toast('请勾选协议')
          console.log('验证通过')
          this.codeAvailable = true
          console.log(this.model.name)
          console.log(this.model.courseType)
          console.log(this.model.classType)
          console.log(this.model.classCode)
          this.$u.route({
            params: this.model,
          	url: '/pages/NewClassConfirm/NewClassConfirm'
          })
        } else {
          console.log('验证失败')
        }
      })
    },
    // 勾选版权协议
    checkboxChange (e) {
      this.model.agreement = e.value
    }
  }
};
</script>

<style scoped lang="scss">
  .wrap {
    padding: 30rpx;
  }

  .agreement {
    display: flex;
    align-items: center;
    margin: 40rpx 0;

    .agreement-text {
      padding-left: 8rpx;
      color: $u-tips-color;
    }
  }
</style>
