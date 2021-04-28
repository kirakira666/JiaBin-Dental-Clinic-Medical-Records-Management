<template>
  <view>
    <view class="work-type">
      <u-field :type="textarea" :password="false" @click="selectShow = true" v-model="workType" :disabled="true" label="作业类型"
        right-icon="arrow-down-fill">
      </u-field>
      <u-field :type="textarea" @click="sessionShow = true" v-model="session" :disabled="true" label="请选择课节课次"
        placeholder="请选择课节课次" right-icon="arrow-down-fill">
      </u-field>
    </view>
    <u-field :type="textarea" v-model="title" label="作业标题" placeholder="请在此输入作业标题">
    </u-field>
    <view v-if="workType === '普通作业'">
      <u-field :type="textarea" @click="showCalender = true" v-model="dueDay" :disabled="true" label="请选择提交截止日期"
        placeholder="请点击选择提交截止日期" right-icon="arrow-down-fill">
      </u-field>
      <u-field :type="textarea" @click="showTime = true" v-model="dueTime" :disabled="true" label="请选择提交截止时间"
        placeholder="请点击选择提交截止时间" right-icon="arrow-down-fill">
      </u-field>
    </view>
    <view v-if="workType === '测试'">
      <u-field :type="textarea" @click="showRegCalender = true" v-model="regulDay" :disabled="true" label="请选择定时发布的日期"
        placeholder="请点击选择定时发布的日期" right-icon="arrow-down-fill">
      </u-field>
      <u-field :type="textarea" @click="showRegTime = true" v-model="regulTime" :disabled="true" label="请选择定时发布的时间"
        placeholder="请点击选择定时发布的时间" right-icon="arrow-down-fill">
      </u-field>
      <u-field :type="textarea" @click="showTest = true" v-model="testTime" :disabled="true" label="请选择测试时长"
        placeholder="请点击选择测试时长" right-icon="arrow-down-fill">
      </u-field>
    </view>
    <u-row>
      <u-col span="5">
        <text>已选择学生人数：</text>{{chooseCount}}
      </u-col>
      <u-col span="4">
        <text>未选择学生人数：</text>{{leftCount}}
      </u-col>
      <u-col span="3">
        <u-button @click="chooseStudent">选学生</u-button>
      </u-col>
    </u-row>
    <view v-for="(item, index) in problem" :key=index>
      <u-row>
        <u-col span="10">
          <problem-list></problem-list>
        </u-col>
        <u-col span="2">
          <u-button>预览</u-button>
          <u-button>删除</u-button>
        </u-col>
      </u-row>
    </view>
    <view>
      <u-row>
        <u-col span="4">
          <text>选择题库</text>
        </u-col>
        <u-col span="8">
          <u-button><strong>+</strong></u-button>
        </u-col>
      </u-row>
      <u-row>
        <u-col span="6">
          <u-button>预览</u-button>
        </u-col>
        <u-col span="6">
          <u-button>确认发布</u-button>
        </u-col>
      </u-row>
    </view>
    <u-select mode="single-column" :list="selectList" v-model="selectShow" @confirm="selectConfirm"></u-select>
    <u-select mode="mutil-column-auto" :list="sessionList" v-model="sessionShow" @confirm="confirmSession"></u-select>
    <u-calendar v-model="showCalender" :mode="calenderMode" @change="setDueDay" :min-date="minDate" :max-date="maxDate">
      <view slot="tooltip">
        <view class="title">
          请选择作业提交的截止日期
        </view>
      </view>
    </u-calendar>
    <u-calendar v-model="showRegCalender" :mode="calenderMode" @change="setRegulDay" :min-date="minDate" :max-date="maxDate">
      <view slot="tooltip">
        <view class="title">
          请选择测试的定时发布时间
        </view>
      </view>
    </u-calendar>
    <u-popup v-model="showTime" mode="center" closeable="true">
      <view>
        <view>请选择或在输入框输入截止时间</view>
        <u-number-box v-model="dueHour" :min="0" :max="59"></u-number-box>时
        <u-number-box v-model="dueMini" :min="0" :max="59"></u-number-box>分
        <u-number-box v-model="dueSecond" :min="0" :max="59"></u-number-box>秒
        <u-button @click="setDueTime">确定</u-button>
      </view>
    </u-popup>
    <u-popup v-model="showTest" mode="center" closeable="true">
      <view>
        <view>请选择或在输入框输入预计测试时长</view>
        <u-number-box v-model="testHour" :min="0" :max="3"></u-number-box>时
        <u-number-box v-model="testMini" :min="0" :max="59"></u-number-box>分
        <u-button @click="setTestTime">确定</u-button>
      </view>
    </u-popup>
    <u-popup v-model="showRegTime" mode="center" :closeable="true">
      <view>
        <h>请选择或在输入框输入预计发布时间</h>
        <u-number-box v-model="regulHour" :min="0" :max="3"></u-number-box>时
        <u-number-box v-model="regulMini" :min="0" :max="59"></u-number-box>分
        <u-button @click="setRegulTime">确定</u-button>
      </view>
    </u-popup>
    <u-popup v-model="chooseShow" mode="left" :closeable="false" @open="tempCount">
      <view>
        <view>
          请选择要发布作业的学生
        </view>
        <view>
          <u-row>
            <u-col span="4.5">
              <text>已选择学生人数：</text>{{tempChoose.chooseCount}}
            </u-col>
            <u-col span="4.5">
              <text>未选择学生人数：</text>{{tempChoose.leftCount}}
            </u-col>
            <u-col span="3">
              <u-checkbox-group>
                <u-checkbox @change="chooseAll" v-model="all" :value="12">
                  全选
                </u-checkbox>
              </u-checkbox-group>
            </u-col>
          </u-row>
          <u-checkbox-group @change="checkboxGroupChange" :wrap="true">
            <u-checkbox @change="checkboxChange" v-model="item.checked" v-for="(item, index) in studentList" :key="index"
              :name="item.name">
              <u-avatar></u-avatar>
              {{item.name}}
            </u-checkbox>
          </u-checkbox-group>
          <view>
            <u-row>
              <u-col span="6">
                <u-button @click="cancelCount"> 取消</u-button>
              </u-col>
              <u-col span="6">
                <u-button @click="confirmCount">
                  确定
                </u-button>
              </u-col>
            </u-row>
          </view>
        </view>
      </view>
    </u-popup>
  </view>
</template>

<script>
  import ProblemList from '../../components/ProblemList/ProblemList.vue'
  export default {
    data() {
      return {
        isCommon: true,
        title: '',
        time: '',
        dueDay: '',
        all: false,
        dueTime: '',
        workType: '普通作业',
        border: false,
        session: '第一单元 第一次',
        sessionShow: false,
        showCalender: false,
        chooseShow: false,
        showTime: false,
        showRegCalender: false,
        showRegTime: false,
        showTest: false,
        time: '',
        selectShow: false,
        dueHour: 0,
        dueMini: 0,
        dueSecond: 0,
        dueTime: '',
        testHour: 0,
        testMini: 0,
        testTime: '',
        regulHour: 0,
        regulMini: 0,
        regulTime: '',
        regulDay: '',
        calenderMode: 'date',
        minDate: '2020-07-16',
        maxDate: '2030-07-16',
        chooseCount: 0,
        leftCount: 0,
        studentCount: 0,
        tempChoose: {
          leftCount: 0,
          chooseCount: 0
        },
        selectList: [{
          label: '普通作业',
          value: 0
        }, {
          label: '测试',
          value: 1
        }],
        sessionList: [

        ],
        problem: [
          '1',
          '2',
          '3'
        ],
        studentList: [{
            name: 'xiaoming',
            checked: false,
            tempchecked: false,
            disabled: false
          },
          {
            name: 'lihua',
            checked: false,
            tempchecked: false,
            disabled: false
          },
          {
            name: 'lily',
            checked: false,
            tempchecked: false,
            disabled: false
          }
        ]
      }
    },
    components: {
      ProblemList
    },
    mounted() {
      let value = 2
      const left = ['第一单元', '第二单元', '第三单元']
      const right = [
        ['第一次', '第二次', '第三次'],
        ['第一次', '第二次'],
        ['第一次', '第二次', '第三次', '第三次']
      ]
      let temp = []
      for (let i = 0; i < left.length; i++) {
        for (let j = 0; j < right[i].length; j++) {
          temp.push({
            label: right[i][j],
            value: value++
          })
        }
        this.sessionList.push({
          label: left[i],
          value: value++,
          children: temp
        })
        temp = []
        // 不能用temp.length=0， 这样会改变children里面temp的值
      }
      const time = new Date()
      this.title = (time.getMonth() + 1) + '月' + time.getDate() + '日  ' + this.session
      this.studentCount = this.studentList.length
      this.leftCount = this.studentList.length
    },
    methods: {
      selectConfirm(e) {
        this.workType = e[0].label
      },
      setDueDay(e) {
        console.log(e)
        this.dueDay = e.year + ' 年' + e.mongth + ' 月' + e.day + ' 日'
      },
      chooseStudent() {
        this.chooseShow = true
      },
      confirmSession(e) {
        this.session = e[0].label + '  ' + e[1].label
        const time = new Date()
        this.title = (time.getMonth() + 1) + '月' + time.getDate() + '日  ' + this.session
      },
      setDueTime() {
        this.showTime = false
        this.dueTime = this.dueHour + '时' + this.dueMini + '分' + this.dueSecond + '秒'
      },
      setTestTime() {
        this.showTest = false
        this.testTime = this.testHour + '时' + this.testMini + '分'
      },
      setRegulDay(e) {
        this.regulDay = e.year + ' 年' + e.month + ' 月' + e.day + ' 日'
      },
      setRegulTime() {
        this.showRegTime = false
        this.regulTime = this.regulHour + '时' + this.regulMini + '分'
      },
      // 选中某个复选框时，由checkbox时触发
      checkboxChange(e) {
        // console.log('checkobox' + e);
      },
      // 选中任一checkbox时，由checkbox-group触发
      checkboxGroupChange(e) {
        this.tempChoose.chooseCount = e.length
        this.tempChoose.leftCount = this.studentCount - this.tempChoose.chooseCount
        if (e.length !== this.studentCount) {
          // 没有全选则取消全选选项
          this.all = false
        } else {
          // 全选则显示全选
          this.all = true
        }
      },
      chooseAll(e) {
        console.log(e)
        if (e.value) {
          this.all = true
          this.studentList.map(item => this.$set(item, 'checked', true))
          this.tempChoose.chooseCount = this.studentCount
          this.tempChoose.leftCount = 0
        } else {
          this.studentList.map(item => this.$set(item, 'checked', false))
          this.all = false
          this.tempChoose.chooseCount = 0
          this.tempChoose.leftCount = this.studentCount
        }
      },
      tempCount () {
        this.tempChoose.leftCount = this.leftCount
        this.tempChoose.chooseCount = this.chooseCount
        for (let i = 0; i < this.studentCount; i++) {
          this.studentList[i].checked=this.studentList[i].tempchecked
        }
        if (this.chooseCount === this.studentCount) {
          this.all = true
        } else {
          this.all = false
        }
      },
      confirmCount () {
        this.chooseShow = false
        this.leftCount = this.tempChoose.leftCount
        this.chooseCount = this.tempChoose.chooseCount
        for (let i = 0; i < this.studentCount; i++) {
          this.studentList[i].tempchecked=this.studentList[i].checked
        }
      },
      cancelCount () {
        this.chooseShow = false
        for (let i = 0; i < this.studentCount; i++) {
          this.studentList[i].checked=this.studentList[i].tempchecked
        }
      }
    },
  }
</script>

<style scoped>
  .title {
    color: $u-type-primary;
    text-align: center;
    padding: 20rpx 0 0 0;
  }
</style>
