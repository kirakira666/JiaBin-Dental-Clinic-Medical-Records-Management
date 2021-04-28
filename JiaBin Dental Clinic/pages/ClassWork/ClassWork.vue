<template>
  <view>
    <tea-class></tea-class>
    <view>
      <button>新发布作业</button>
    </view>
    <class-work-info></class-work-info>
  </view>
</template>

<script>
  import TeaClass from '../../components/TeaClass/TeaClass.vue'
  import ClassWorkInfo from '../../components/ClassWorkInfo/ClassWorkInfo.vue'
  export default {
    data() {
      return {

      }
    },
    components: {
      TeaClass,
      ClassWorkInfo
    },
    methods: {

    }
  }
</script>

<style>

</style>
