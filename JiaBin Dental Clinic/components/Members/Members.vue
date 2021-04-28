<template>
  <view class="" v-show="Inv == 0">
    <!-- 班级成员Members -->
    <u-cell-group title-bg-color="rgb(243, 244, 246)" :title="item.groupName" v-for="(item, index) in list" :key="index">
      <u-cell-item :titleStyle="{fontWeight: 500}" @click="openPage(item1.path)" v-for="(item1, index1) in item.list"
        :key="index1">
<!--        <image slot="icon" class="u-cell-icon" :src="getIcon(item1.icon)" mode="widthFix"></image> -->
        <class-member></class-member>
      </u-cell-item>
    </u-cell-group>
  </view>
</template>

<script>
import ClassMember from '../../components/ClassMember/ClassMember.vue'
export default {
  data () {
    return {
      Inv: 0,
      title: '班级成员',
      mode: 'circle',
      text: '', // 优先级比src高
      size: '90',
      list: [{
        groupName: '老师',
        list: [{
          path: '/pages/Center/Center',
          icon: 'tag',
          title: '刘老师'
        }, {
        path: '/pages/Center/Center',
          icon: 'tag',
          title: '李老师'
        }]
      },
      {
        groupName: '学生',
        list: [{
          path: '/pages/StuCenter/StuCenter',
          icon: 'form',
          title: 's1'
        },{
          path: '/pages/StuCenter/StuCenter',
          icon: 'form',
          title: 's2'
        }]
      }
      ],
       list2: [{
        groupName: '作业提交情况',
        list2: [{
          path: '/pages/TeaStuAllWork/TeaStuAllWork',
          icon: 'form',
          title: '小刘'
        }, {
          path: '/pages/TeaStuAllWork/TeaStuAllWork',
          icon: 'form',
          title: '小李'
        },{
          path: '/pages/TeaStuAllWork/TeaStuAllWork',
          icon: 'form',
          title: 's2'
          }, {
          path: '/pages/TeaStuAllWork/TeaStuAllWork',
          icon: 'form',
          title: 's2'
          }]
        }]
      }
    },
    computed: {
      getIcon() {
        return path => {
          return 'https://cdn.uviewui.com/uview/example/' + path + '.png'
        }
      }
    },
    components: {
      ClassMember
    },
    methods: {
      openPage (path) {
        this.$u.route({
          url: path
        })
      }
    }
  }
</script>

<style lang="scss" scoped>
  .u-cell-icon {
    height: 40rpx;
    width: 40rpx;
  }
</style>
