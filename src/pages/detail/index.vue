<template>
  <view class="temple-detail">
    <view class="info-image">
		<image src="../../static/temple.png" mode="widthFix"></image>
	</view>
    <!-- 基本信息 -->
    <view class="content-section">
      <rich-text :nodes="templeInfo.content"></rich-text>
    </view>
    
  </view>
</template>

<script>
export default {
  data() {
    return {
      templeInfo: {
        name: '某某寺',
        location: 'xx省xx市xx区',
        images: [
          '/static/temple/detail1.jpg',
          '/static/temple/detail2.jpg'
        ],
        content: '<div>某某寺位于xx山，始建于唐代，为国家重点文物保护单位...</div>',
        openTime: [
          { label: '夏季', value: '06:00-18:00' },
          { label: '冬季', value: '07:00-17:00' }
        ],
        traffic: [
          '地铁：乘坐x号线至xx站下车',
          '公交：乘坐xx路公交车至xx站下车',
          '自驾：导航至xx路xx号'
        ]
      }
    }
  },
  onLoad(options) {
    // TODO: 根据id获取寺庙详情
    const { id, title = title || '默认标题' } = options
	  uni.setNavigationBarTitle({
	    title: title
	  });
  }
}
</script>

<style lang="scss" scoped>
.temple-detail {
  .info-image {
	  image {
		  width: 100%;
	  }
  }
  .content-section {
    padding: 2upx 20upx;
	color: rgba(79,79,79,1);
	font-size: 28upx;
	font-family: AlibabaPuHui-regular;
  }
}
</style> 