<template>
  <view class="activity-list">
    <!-- 活动列表 -->
    <view class="list-content">
      <view 
        class="activity-item"
        v-for="(item, index) in activityList"
        :key="index"
        @tap="goDetail(item.id)"
      >
        <image class="cover" :src="item.image" mode="widthFix"></image>
        <view class="info font-bold">
          <!-- <view class="title">{{item.title}}</view> -->
            <view class="time">{{item.time}}</view>
          <view class="desc">{{item.desc}}</view>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      activityList: [
        {
          id: 1,
          title: '冬季禅修营',
          desc: '为期7天的禅修活动，由知名法师亲自指导',
          time: '2024-01-15 ~ 2024-01-21',
          status: 'enrolling',
          image: '/static/activity/1.jpg'
        }
      ],
    }
  },
  onLoad() {
    this.getActivityList()
  },
  methods: {
    async getActivityList() {
      this.loadMoreStatus = 'loading'
      // TODO: 调用接口获取活动列表
      setTimeout(() => {
        const statusArr = ['enrolling', 'full', 'end']
        const list = [...Array(10)].map((_, i) => ({
          id: this.page * 10 + i,
          title: `活动${this.page * 10 + i}`,
          desc: '一场有意思的长袖活动',
          time: '2024-01-15 ~ 2024-01-21',
          status: statusArr[Math.floor(Math.random() * 3)],
          image: '/static/activity.png'
        }))
        
        this.activityList = [...this.activityList, ...list]
      }, 1000)
    },
    goDetail(id) {
      uni.navigateTo({
        url: `/pages/detail/index?id=${id}&title=活动详情`
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.activity-list {
  min-height: 100vh;
  
  .list-content {
    .activity-item {
		position: relative;
		margin-bottom: 40upx;
		overflow: hidden;
      
      .cover {
        width: 100%;
        height: 580upx;
      }
      
      .info {
		position: absolute;
		bottom: 0;
		width: 100%;
		height: 122upx;
		padding: 16rpx 0;
		font-size: 32upx;
		background-color: rgba(255,255,255, 0.5);
        box-sizing: border-box;
		
        .desc {
			padding-right: 48upx;
			text-align: right;
			background: url('@/static/icons/icon-right-arrow.png') no-repeat;
			background-position: right;
			background-size: contain;
        }
        
		.time {
			margin-left: 8upx;
			line-height: 44upx;
		}
      }
    }
  }
}
</style> 