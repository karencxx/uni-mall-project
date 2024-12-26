<template>
  <view class="pray">
    <ModulesComp :modules="prayList"></ModulesComp>
  </view>
</template>

<script>
import ModulesComp from '@/components/ModulesComp.vue'
const modulesList = [
  {
    name: '丝带祈福',
    image: '/static/pray/ribbon.png',
    path: '/pages/pray/detail?type=ribbon'
  },
  {
    name: '福牌祈福',
    image: '/static/pray/plate.png',
    path: '/pages/pray/detail?type=plate'
  },
  {
    name: '供灯祈福',
    image: '/static/pray/lamp.png',
    path: '/pages/pray/detail?type=lamp'
  },
  {
    name: '法事祈福',
    image: '/static/pray/ritual.png',
    path: '/pages/pray/detail?type=ritual'
  },
  {
    name: '放生祈福',
    image: '/static/pray/release.png',
    path: '/pages/pray/detail?type=release'
  },
  {
    name: '供奉佛像',
    image: '/static/pray/buddha.png',
    path: '/pages/pray/detail?type=buddha'
  }
]
export default {
  components:{
	ModulesComp
  },
  data() {
    return {
      prayList: modulesList
    }
  },
  methods: {
    navigateTo(path) {
      uni.navigateTo({
        url: path
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.pray {
  padding: 20rpx;
  
  .pray-list {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    
    .pray-item {
      width: 345rpx;
      height: 200rpx;
      margin-bottom: 20rpx;
      position: relative;
      border-radius: 10rpx;
      overflow: hidden;
      
      image {
        width: 100%;
        height: 100%;
      }
      
      text {
        position: absolute;
        bottom: 20rpx;
        left: 20rpx;
        color: #fff;
        font-size: 28rpx;
      }
    }
  }
}
</style> 