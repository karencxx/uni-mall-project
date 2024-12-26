<template>
    <view class="recommend-container">
        <view class="title">为你推荐</view>
        <view class="list">
          <view class="item" v-for="(item, index) in list" :key="index">
            <image :src="item.image" mode="aspectFill"></image>
            <text>{{ item.name }}</text>
          </view>
        </view>
      </view>
</template>


<script>
export default {
    data(){
		return {
			list: []
		}
	},
    mounted() {
        this.getRecommendList()
    },
    methods: {
      getRecommendList() {
      // this.$api.getRecommendList().then(res => {
        this.list = [
          {
            image: '',
            name: '丝带祈福'
          },
          {
            image: '',
            name: '五福手串'
          },
          {
            image: '',
            name: '舅子离火手串'
          },
          {
            image: '',
            name: '舅子离火手串'
          }
        ]
      // })
      }
  }
}
</script>

<style lang="scss" scoped>
.recommend-container {
    padding: 28upx 52rpx;
    
    .title {
      font-size: 36upx;
      font-weight: bold;
      line-height: 52upx;
      color: rgba(51,51,51,1);
      font-family: PingFangSC-bold;
    }
    
    .list {
      display: flex;
      flex-wrap: wrap;
      margin: 16upx 32upx 0;
      column-gap: 60upx;
      text-align: center;
      
      .item {
        max-width: 144upx;
        margin-right: 10rpx;
        margin-bottom: 10rpx;
        
        image {
          width: 100upx;
          height: 124upx;
          border: 1px solid;
        }
        
        text {
          display: block;
          font-size: 24upx;
          text-align: center;
          line-height: 36upx;
        }
      }
    }
  }
</style>>
