<template>
  <view class="index">
    <!-- 顶部轮播 -->
    <swiper class="banner" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
      <block v-for="(item, index) in bannerList" :key="index">
        <swiper-item>
          <image :src="item.url" mode="aspectFill"></image>
        </swiper-item>
      </block>
    </swiper>
    
    <!-- 功能模块 -->
    <ModulesComp :modules="modules"></ModulesComp>
    
    <!-- 为你推荐 -->
    <RecommendList :data="recommendList"></RecommendList>
  </view>
</template>

<script>
import ModulesComp from '@/components/ModulesComp.vue'
import RecommendList from '@/components/RecommendList.vue'

const modulesList = [
  {
    name: '了解寺庙',
    icon: '/static/icons/icon-home.png',
    path: '/pages/temple/list'
  },
  {
    name: '禅修活动',
    icon: '/static/icons/icon-activity.png',
    path: '/pages/activity/list'
  },
  {
    name: '祈福许愿',
    icon: '/static/icons/icon-pray.png',
    path: '/pages/pray/index',
	navigateTo: 'tab'
  },
  {
    name: '法物流通',
    icon: '/static/icons/icon-shop.png',
    path: '/pages/shop/index',
	navigateTo: 'tab'
  }
]
export default {
  components: {
    ModulesComp,
    RecommendList
  },
  data() {
    return {
      bannerList: [],
      modules: modulesList,
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
.index {
  .banner {
    width: 750rpx;
    height: 400rpx;
    image {
      width: 100%;
      height: 100%;
    }
  }
}
</style> 