<template>
  <view class="pray-detail">
	  <Barrage :list="barrageList"></Barrage>
    <!-- 商品大图 -->
    <swiper class="swiper" :indicator-dots="true" :autoplay="true">
      <swiper-item v-for="(item, index) in goodsImages" :key="index">
        <image :src="item" mode="aspectFill"></image>
      </swiper-item>
    </swiper>
    <!-- 商品信息 -->
    <view class="goods-info">
      <view class="desc">{{goodsInfo.desc}}</view>
    </view>
	
	<!-- 注意事项 -->
	<view class="notice release">
	    <view class="font-bold">本次放生日期</view>
	    <text class="content">佛历时间：2567年十一月二十 农历时间：2024年十一月二十
		公历时间：2024年12月20日
		</text>
	</view>
	
	<!-- 底部按钮 -->
	<view class="footer">
		<view class="footer-left">
			<view name="release-info" class="release-info font-bold">本月祈福截止时间：<text class="release-date">12月19日</text></view>
			<view class="common-info">祈福成功后，寺庙会发送一条专属您的祈福视频</view>
		</view>
		<button class="pray-btn" @tap.native.stop="showSkuPopup">立即祈福</button>
	</view>
   
    <!-- SKU弹窗 -->
    <SkuComp
      ref="skuComp"
      :goodsInfo="goodsInfo"
      :skuList="skuList"
      @confirm="handleSkuConfirm"
    >
		<template #release>
			<view class="release-info font-bold release-info-right">本月祈福截止时间：<text class="release-date">12月19日</text></view>
		</template>
	</SkuComp>
  </view>
</template>

<script>
import SkuComp from '@/components/SkuComp.vue'
import Barrage from '@/components/Barrage.vue'
export default {
  components: {
    SkuComp,
	Barrage
  },
  data() {
    return {
      goodsImages: [
        '/static/logo.png',
        '/static/temple.png'
      ],
      barrageList: [
        '宁波的张三，祈福成功',
        '李四,祈福成功',
        '王五刚刚祈福了',
        '张家界的王五，刚刚祈福了',
        '王五刚刚祈福了',
      ],
      goodsInfo: {
        price: 99,
        title: '丝带祈福',
        desc: '丝带祈福是一种传统的祈福方式，将美好的祝愿系在丝带上...',
        image: '/static/logo.png'
      },
      skuList: [
        {id: 1, name: '款式一', price: 1990, image: '/static/logo.png'   },
        {id: 2, name: '事业祈福', price: 290, image: '/static/logo.png'},
        {id: 3, name: '款式二', price: 1000, image: '/static/logo.png'},
        {id: 4, name: '健康祈福', price: 1000, image: '/static/logo1.png'}
      ],
    }
  },
  methods: {
    showSkuPopup() {
      this.$refs.skuComp.open()
    },
    handleSkuConfirm({sku, num}) {
      uni.navigateTo({
        url: `/pages/pray/order?skuId=${sku.id}&num=${num}`
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.pray-detail {
  padding-bottom: 200upx;
  
  .swiper {
    width: 100%;
    height: 750upx;
    
    image {
      width: 100%;
      height: 100%;
    }
  }
  
  .goods-info {
    padding: 12upx 12upx;
    
    .desc {
      font-size: 36upx;
      color: #333;
      line-height: 48upx;
    }
  }
  
  .notice {
	padding: 0 12upx;
	  
	&.release {
		margin-top: 40upx;
		color: #E99D42;
		font-size: 28upx;
		
		text {
			word-break: break-word;
		}
	}
  }
  
  .footer {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
	height: 120upx;
    display: flex;
    align-items: flex-start;
	justify-content: space-between;
	font-size: 22upx;
	color: #BD3124;
    background: #fff;
	
	.footer-left {
		flex: auto;
		margin: 0 6upx;
		.common-info {
			text-align: right;
		}
	}
    
    .pray-btn {
      width: 208upx;
      height: 80upx;
      line-height: 80upx;
	  margin-right: 20upx;
      background: #BD3124;
      color: #fff;
      font-size: 32upx;
      border-radius: 60upx;
    }
  }
  .release-info {
  	color: #333;
	font-size: 24upx;
	
	&-right {
		text-align: right;
		margin-right: 12upx;
		margin-top: -60upx;
	}
  	.release-date {
  		color: #BD3124;
  	}
  }
}
</style>
