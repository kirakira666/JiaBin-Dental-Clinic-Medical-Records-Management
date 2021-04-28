<template>
	<view class="">
		<wechat-data></wechat-data>
		<view class="wrap">
			<u-form :model="model" :rules="rules" ref="uForm" :errorType="errorType">
				<u-form-item label-width="700" label="8月21日来诊病人诊断书填写:">
				</u-form-item>
				<u-form-item :label-position="labelPosition" label="选择病人" prop="courseType1" label-width="150">
					<u-input :border="border" type="select" :select-open="pickerShow" v-model="model.courseType1" placeholder="请选择病人" @click="selectShow1 = true"></u-input>
				</u-form-item>
        <u-form-item :label-position="labelPosition" label="选择医师" prop="courseType2" label-width="150">
        	<u-input :border="border" type="select" :select-open="pickerShow" v-model="model.courseType2" placeholder="请选择主治医师" @click="selectShow2 = true"></u-input>
        </u-form-item>
        <u-form-item :label-position="labelPosition" label="选择牙位" prop="courseType4" label-width="150">
        	<u-input :border="border" type="select" :select-open="pickerShow" v-model="model.courseType4" placeholder="请选择牙位" @click="selectShow4 = true"></u-input>
        </u-form-item>
        <u-form-item :label-position="labelPosition" label="诊断" prop="intro">
        	<u-input type="textarea" :border="border" placeholder="请填写诊断" v-model="model.intro" />
        </u-form-item>
        <u-form-item :label-position="labelPosition" label="处方" prop="intro2">
        	<u-input type="textarea" :border="border" placeholder="请填写处方" v-model="model.intro2" />
        </u-form-item>
        <u-form-item :label-position="labelPosition" label="备注" prop="intro3">
        	<u-input type="textarea" :border="border" placeholder="此处添加备注" />
        </u-form-item>
        <u-form-item :label-position="labelPosition" label="费用是否缴清" prop="isFirst" label-width="200">
        	<u-radio-group v-model="radio2" @change="radioGroupChange2" :width="radioCheckWidth" :wrap="radioCheckWrap">
        		<u-radio shape="circle" v-model="item.checked" v-for="(item, index) in radioList2" :key="index" :name="item.name">{{ item.name }}</u-radio>
        	</u-radio-group>
        </u-form-item>
			</u-form>
			<u-button type="primary" @click="submit">提交</u-button>
			<u-select mode="mutil-column-auto" :list="selectList1" v-model="selectShow1" @confirm="selectConfirm1"></u-select>
      <u-select mode="mutil-column-auto" :list="selectList2" v-model="selectShow2" @confirm="selectConfirm2"></u-select>
      <u-select mode="mutil-column-auto" :list="selectList4" v-model="selectShow4" @confirm="selectConfirm4"></u-select>
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
        courseType1: '',
				courseType2: '',
        isFirst: '否',
        phone: '',
        intro2: '',
        intro: '',
        intro3: ''
			},
      selectList4: [
      	{
      		label: '无',
      		value: '1',
      		children: [
      			{
      				label: '无',
      				value: '2'
      			},
            {
            	label: '1',
            	value: '2'
            },
      			{
      				label: '2',
      				value: '2'
      			},
            {
            	label: '3',
            	value: '2'
            },
            {
            	label: '4',
            	value: '2'
            },
            {
            	label: '5',
            	value: '2'
            },
            {
            	label: '6',
            	value: '2'
            },
            {
            	label: '7',
            	value: '2'
            },
            {
            	label: '8',
            	value: '2'
            },
            {
            	label: '9',
            	value: '2'
            },
            {
            	label: '10',
            	value: '2'
            },
            {
            	label: '11',
            	value: '2'
            },
            {
            	label: '12',
            	value: '2'
            },
            {
            	label: '13',
            	value: '2'
            },
            {
            	label: '14',
            	value: '2'
            },
            {
            	label: '15',
            	value: '2'
            },
            {
            	label: '16',
            	value: '2'
            }
      		]
      	},
      	{
      		label: '2',
      		value: '1',
      		children: [
      			{
      				label: '无',
      				value: '2'
      			},
      	    {
      	    	label: '1',
      	    	value: '2'
      	    },
      			{
      				label: '2',
      				value: '2'
      			},
      	    {
      	    	label: '3',
      	    	value: '2'
      	    },
      	    {
      	    	label: '4',
      	    	value: '2'
      	    },
      	    {
      	    	label: '5',
      	    	value: '2'
      	    },
      	    {
      	    	label: '6',
      	    	value: '2'
      	    },
      	    {
      	    	label: '7',
      	    	value: '2'
      	    },
      	    {
      	    	label: '8',
      	    	value: '2'
      	    },
      	    {
      	    	label: '9',
      	    	value: '2'
      	    },
      	    {
      	    	label: '10',
      	    	value: '2'
      	    },
      	    {
      	    	label: '11',
      	    	value: '2'
      	    },
      	    {
      	    	label: '12',
      	    	value: '2'
      	    },
      	    {
      	    	label: '13',
      	    	value: '2'
      	    },
      	    {
      	    	label: '14',
      	    	value: '2'
      	    },
      	    {
      	    	label: '15',
      	    	value: '2'
      	    },
      	    {
      	    	label: '16',
      	    	value: '2'
      	    }
      		]
      	},
        {
        	label: '3',
        	value: '1',
        	children: [
        		{
        			label: '无',
        			value: '2'
        		},
            {
            	label: '1',
            	value: '2'
            },
        		{
        			label: '2',
        			value: '2'
        		},
            {
            	label: '3',
            	value: '2'
            },
            {
            	label: '4',
            	value: '2'
            },
            {
            	label: '5',
            	value: '2'
            },
            {
            	label: '6',
            	value: '2'
            },
            {
            	label: '7',
            	value: '2'
            },
            {
            	label: '8',
            	value: '2'
            },
            {
            	label: '9',
            	value: '2'
            },
            {
            	label: '10',
            	value: '2'
            },
            {
            	label: '11',
            	value: '2'
            },
            {
            	label: '12',
            	value: '2'
            },
            {
            	label: '13',
            	value: '2'
            },
            {
            	label: '14',
            	value: '2'
            },
            {
            	label: '15',
            	value: '2'
            },
            {
            	label: '16',
            	value: '2'
            }
        	]
        },
        {
        	label: '4',
        	value: '1',
        	children: [
        		{
        			label: '无',
        			value: '2'
        		},
            {
            	label: '1',
            	value: '2'
            },
        		{
        			label: '2',
        			value: '2'
        		},
            {
            	label: '3',
            	value: '2'
            },
            {
            	label: '4',
            	value: '2'
            },
            {
            	label: '5',
            	value: '2'
            },
            {
            	label: '6',
            	value: '2'
            },
            {
            	label: '7',
            	value: '2'
            },
            {
            	label: '8',
            	value: '2'
            },
            {
            	label: '9',
            	value: '2'
            },
            {
            	label: '10',
            	value: '2'
            },
            {
            	label: '11',
            	value: '2'
            },
            {
            	label: '12',
            	value: '2'
            },
            {
            	label: '13',
            	value: '2'
            },
            {
            	label: '14',
            	value: '2'
            },
            {
            	label: '15',
            	value: '2'
            },
            {
            	label: '16',
            	value: '2'
            }
        	]
        },
        {
        	label: '5',
        	value: '1',
        	children: [
        		{
        			label: '无',
        			value: '2'
        		},
            {
            	label: '1',
            	value: '2'
            },
        		{
        			label: '2',
        			value: '2'
        		},
            {
            	label: '3',
            	value: '2'
            },
            {
            	label: '4',
            	value: '2'
            },
            {
            	label: '5',
            	value: '2'
            },
            {
            	label: '6',
            	value: '2'
            },
            {
            	label: '7',
            	value: '2'
            },
            {
            	label: '8',
            	value: '2'
            },
            {
            	label: '9',
            	value: '2'
            },
            {
            	label: '10',
            	value: '2'
            },
            {
            	label: '11',
            	value: '2'
            },
            {
            	label: '12',
            	value: '2'
            },
            {
            	label: '13',
            	value: '2'
            },
            {
            	label: '14',
            	value: '2'
            },
            {
            	label: '15',
            	value: '2'
            },
            {
            	label: '16',
            	value: '2'
            }
        	]
        },
        {
        	label: '6',
        	value: '1',
        	children: [
        		{
        			label: '无',
        			value: '2'
        		},
            {
            	label: '1',
            	value: '2'
            },
        		{
        			label: '2',
        			value: '2'
        		},
            {
            	label: '3',
            	value: '2'
            },
            {
            	label: '4',
            	value: '2'
            },
            {
            	label: '5',
            	value: '2'
            },
            {
            	label: '6',
            	value: '2'
            },
            {
            	label: '7',
            	value: '2'
            },
            {
            	label: '8',
            	value: '2'
            },
            {
            	label: '9',
            	value: '2'
            },
            {
            	label: '10',
            	value: '2'
            },
            {
            	label: '11',
            	value: '2'
            },
            {
            	label: '12',
            	value: '2'
            },
            {
            	label: '13',
            	value: '2'
            },
            {
            	label: '14',
            	value: '2'
            },
            {
            	label: '15',
            	value: '2'
            },
            {
            	label: '16',
            	value: '2'
            }
        	]
        },
        {
        	label: '7',
        	value: '1',
        	children: [
        		{
        			label: '无',
        			value: '2'
        		},
            {
            	label: '1',
            	value: '2'
            },
        		{
        			label: '2',
        			value: '2'
        		},
            {
            	label: '3',
            	value: '2'
            },
            {
            	label: '4',
            	value: '2'
            },
            {
            	label: '5',
            	value: '2'
            },
            {
            	label: '6',
            	value: '2'
            },
            {
            	label: '7',
            	value: '2'
            },
            {
            	label: '8',
            	value: '2'
            },
            {
            	label: '9',
            	value: '2'
            },
            {
            	label: '10',
            	value: '2'
            },
            {
            	label: '11',
            	value: '2'
            },
            {
            	label: '12',
            	value: '2'
            },
            {
            	label: '13',
            	value: '2'
            },
            {
            	label: '14',
            	value: '2'
            },
            {
            	label: '15',
            	value: '2'
            },
            {
            	label: '16',
            	value: '2'
            }
        	]
        },
        {
        	label: '8',
        	value: '1',
        	children: [
        		{
        			label: '无',
        			value: '2'
        		},
            {
            	label: '1',
            	value: '2'
            },
        		{
        			label: '2',
        			value: '2'
        		},
            {
            	label: '3',
            	value: '2'
            },
            {
            	label: '4',
            	value: '2'
            },
            {
            	label: '5',
            	value: '2'
            },
            {
            	label: '6',
            	value: '2'
            },
            {
            	label: '7',
            	value: '2'
            },
            {
            	label: '8',
            	value: '2'
            },
            {
            	label: '9',
            	value: '2'
            },
            {
            	label: '10',
            	value: '2'
            },
            {
            	label: '11',
            	value: '2'
            },
            {
            	label: '12',
            	value: '2'
            },
            {
            	label: '13',
            	value: '2'
            },
            {
            	label: '14',
            	value: '2'
            },
            {
            	label: '15',
            	value: '2'
            },
            {
            	label: '16',
            	value: '2'
            }
        	]
        },
      	{
      		label: '英语',
      		value: '1',
      		children: [
      			{
      				label: '英语课程2级别',
      				value: '2'
      			}
      		]
      	}
      ],
			selectList1: [
				{
					label: '老刘',
					value: '1',
					
				},
				{
					label: '老王',
					value: '1',
					
				}
			],
      selectList2: [
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
				intro: [
					{
						required: true,
						message: '请输入诊断',
						trigger: 'blur' ,
					}
				],
        intro2: [
        	{
        		required: true,
        		message: '请输入处方',
        		trigger: 'blur' ,
        	}
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
				courseType1: [
					{
						required: true,
						message: '请选择就诊病人',
						trigger: 'change',
					}
				],
        courseType4: [
        	{
        		required: true,
        		message: '请选择牙位',
        		trigger: 'change',
        	}
        ],
        courseType2: [
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
      radio2: '否',
			pickerShow: false,
			selectShow1: false,
      selectShow2: false,
      selectShow4: false,
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
		selectConfirm1(e) {
			this.model.courseType1 = ''
			e.map((val, index) => {
				this.model.courseType1 += this.model.courseType1 == '' ? val.label : val.label
			})
		},
    selectConfirm2(e) {
    	this.model.courseType2 = ''
    	e.map((val, index) => {
    		this.model.courseType2 += this.model.courseType == '' ? val.label : val.label
    	})
    },
    selectConfirm4(e) {
			this.model.courseType4 = ''
			e.map((val, index) => {
				this.model.courseType4 += this.model.courseType4 == '' ? val.label : '-' + val.label
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
