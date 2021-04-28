<template>
	<view class="">
		<wechat-data></wechat-data>
		<view class="wrap">
			<u-form :model="model" :rules="rules" ref="uForm" :errorType="errorType">
				<u-form-item label-width="700" label="8月21日来诊病人信息填写:">
				</u-form-item>
				<u-form-item label-width="120" :label-position="labelPosition" label="姓名" prop="name">
					<u-input :border="border" placeholder="请输入姓名" v-model="model.name" type="text"></u-input>
				</u-form-item>
				<u-form-item :label-position="labelPosition" label="性别" prop="classType2" label-width="150">
					<u-radio-group v-model="radio1" @change="radioGroupChange1" :width="radioCheckWidth" :wrap="radioCheckWrap">
						<u-radio shape="circle" v-model="item.checked" v-for="(item, index) in radioList" :key="index" :name="item.name">{{ item.name }}</u-radio>
					</u-radio-group>
				</u-form-item>
        <u-form-item :label-position="labelPosition" label="是否初诊" prop="isFirst" label-width="150">
        	<u-radio-group v-model="radio2" @change="radioGroupChange2" :width="radioCheckWidth" :wrap="radioCheckWrap">
        		<u-radio shape="circle" v-model="item.checked" v-for="(item, index) in radioList2" :key="index" :name="item.name">{{ item.name }}</u-radio>
        	</u-radio-group>
        </u-form-item>
				<u-form-item :label-position="labelPosition" label="选择医师" prop="courseType" label-width="150">
					<u-input :border="border" type="select" :select-open="pickerShow" v-model="model.courseType" placeholder="请选择主治医师" @click="selectShow = true"></u-input>
				</u-form-item>
        <u-form-item :rightIconStyle="{color: '#888', fontSize: '32rpx'}" right-icon="kefu-ermai" :label-position="labelPosition" label="手机号码" prop="phone" label-width="150">
        	<u-input :border="border" placeholder="请输入手机号" v-model="model.phone" type="number"></u-input>
        </u-form-item>
			</u-form>
			<view class="agreement">
				<u-checkbox v-model="check" @change="checkboxChange"></u-checkbox>
				<view class="agreement-text">
					勾选代表同意我们的医疗信息使用协议
				</view>
			</view>
			<u-button type="primary" @click="submit">提交</u-button>
			<u-select mode="mutil-column-auto" :list="selectList" v-model="selectShow" @confirm="selectConfirm"></u-select>
		</view>
	</view>
</template>

<script>
import WechatData from '../../components/WechatData/WechatData'
export default {
	data() {
		let that = this;
		return {
			model: {
				name: '',
				classType: '男',
				agreement: false,
				courseType2: '',
        isFirst: '是',
        phone: '',
			},
			selectList: [
				{
					label: '刘医生',
					value: '1',
					
				},
				{
					label: '李医生',
					value: '1',
					
				}
			],
			rules: {
				name: [
					{
						required: true,
						message: '请输入姓名',
						trigger: 'blur' ,
					},
					{
						min: 1,
						max: 20,
						message: '姓名长度在3到20个字符',
						trigger: ['change','blur'],
					}
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
        phone: [
        	{
        		required: true,
        		message: '请输入手机号',
        		trigger: ['change','blur'],
        	},
        	{
        		validator: (rule, value, callback) => {
        			// 调用uView自带的js验证规则，详见：https://www.uviewui.com/js/test.html
        			return this.$u.test.mobile(value);
        		},
        		message: '手机号码不正确',
        		// 触发器可以同时用blur和change，二者之间用英文逗号隔开
        		trigger: ['change','blur'],
        	}
        ],
				classType: [
					{
						required: true,
						message: '请选择班级模式',
						trigger: 'change',
					}
				],
				courseType: [
					{
						required: true,
						message: '请选择主治医师',
						trigger: 'change',
					}
				]
			},
			border: false,
			check: false,
			selectStatus: 'close',
			radioList: [
				{
					name: '男',
					checked: true,
					disabled: false
				},
				{
					name: '女',
					checked: false,
					disabled: false
				}
			],
      radioList2: [
      	{
      		name: '是',
      		checked: true,
      		disabled: false
      	},
      	{
      		name: '否',
      		checked: false,
      		disabled: false
      	}
      ],
			radio1: '男',
      radio2: '是',
			pickerShow: false,
			selectShow: false,
			radioCheckWidth: 'auto',
			radioCheckWrap: false,
			labelPosition: 'left',
			codeTips: '',
			errorType: ['message']
		}
	},
	components: {
		WechatData
	},
	onLoad() {

	},
	computed: {
		borderCurrent() {
			return this.border ? 0 : 1
		}
	},
	onReady() {
		this.$refs.uForm.setRules(this.rules)
	},
	methods: {
		submit() {
			this.$refs.uForm.validate(valid => {
				if (valid) {
					if(!this.model.agreement) return this.$u.toast('请勾选协议')
					console.log('验证通过')
					console.log(this.model.name)
					console.log(this.model.classType)
					console.log(this.model.courseType)
          console.log('去往确认界面')
          this.$u.route({
            params: this.model,
          	url: '/pages/NewClassConfirm/NewClassConfirm'
          })
				} else {
					console.log('验证失败')
				}
			})
		},
		// radio选择发生变化
		radioGroupChange1(e) {
			this.model.classType = e
		},
    radioGroupChange2(e) {
    	this.model.isFirst = e
    },
		// 勾选版权协议
		checkboxChange(e) {
			this.model.agreement = e.value
		},
		// 选择商品类型回调
		selectConfirm(e) {
			this.model.courseType = ''
			e.map((val, index) => {
				this.model.courseType += this.model.courseType == '' ? val.label : '-' + val.label
			})
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
