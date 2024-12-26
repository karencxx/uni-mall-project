<template>
  <view class="temple-list-container">
    <view class="list-container">
      <view 
        class="temple-item"
        v-for="(item, index) in templeList"
        :key="index"
        @tap="goDetail(item)"
      >
        <image :src="item.image" mode="aspectFill"></image>
		<view class="tag font-bold">{{ item.tag }}</view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      templeList: [
        {
          id: 1,
          name: '某某寺',
          desc: '某某寺位于xx山，始建于唐代，为国家重点文物保护单位...',
          location: 'xx省xx市',
		  tag: '寺庙介绍',
          image: '/static/temple.png'
        },{
          id: 2,
          name: '某某寺',
          desc: '某某寺位于xx山，始建于唐代，为国家重点文物保护单位...',
          location: 'xx省xx市',
		  tag: '祈福许愿指南',
          image: '/static/temple.png'
        }
      ]
    }
  },
  onLoad() {
    this.getTempleList()
  },
  methods: {
    async getTempleList() {
      this.loadMoreStatus = 'loading'
      // TODO: 调用接口获取寺庙列表
      setTimeout(() => {
        // 模拟数据
        const list = [...Array(4)].map((_, i) => ({
          id: this.page * 10 + i,
          name: `某某寺${this.page * 10 + i}`,
          desc: '某某寺位于xx山，始建于唐代，为国家重点文物保护单位...',
          location: 'xx省xx市',
          image: '/static/temple/1.jpg'
        }))
        
        this.templeList = [...this.templeList, ...list]
        this.loadMoreStatus = list.length < 10 ? 'noMore' : 'more'
      }, 1000)
    },
    goDetail(data) {
		const { id, tag } = data
		uni.navigateTo({
		url: `/pages/detail/index?id=${id}&title=${tag}`
		})
    }
  },
  
}
</script>

<style lang="scss" scoped>
.temple-list-container {
  min-height: 100vh;
  background: #fff;
  padding-bottom: 20rpx;
  
  .list-container {
    column-count: 1;
    column-gap: 26upx;
    
	.temple-item {
		position: relative;
		
		  image {
			width: 100%;
			height: 716upx;
		  }
		  .tag {
			  position: absolute;
			  right: 12upx;
			  bottom: 24upx;
			  width: 236upx;
			  height: 60upx;
			  line-height: 60upx;
			  border-radius: 8upx;
			  background-color: rgba(189,49,36,1);
			  color: rgba(255,255,255,1);
			  font-size: 32upx;
			  text-align: center;
		  }
    }
  }
}
</style> 