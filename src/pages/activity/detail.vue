<template>
  <view class="activity-detail">
    <!-- 活动封面 -->
    <image class="cover" :src="activityInfo.image" mode="aspectFill"></image>
    
    <!-- 活动信息 -->
    <view class="info-section">
      <view class="title">{{activityInfo.title}}</view>
      <view class="status" :class="activityInfo.status">
        {{statusText[activityInfo.status]}}
      </view>
      
      <!-- 基本信息 -->
      <view class="basic-info">
        <view class="info-item">
          <text class="label">活动时间</text>
          <text class="value">{{activityInfo.time}}</text>
        </view>
        <view class="info-item">
          <text class="label">活动地点</text>
          <text class="value">{{activityInfo.location}}</text>
        </view>
        <view class="info-item">
          <text class="label">报名人数</text>
          <text class="value">{{activityInfo.enrollCount}}/{{activityInfo.maxCount}}人</text>
        </view>
        <view class="info-item">
          <text class="label">活动费用</text>
          <text class="value">{{activityInfo.fee > 0 ? '¥' + activityInfo.fee : '免费'}}</text>
        </view>
      </view>
    </view>
    
    <!-- 活动详情 -->
    <view class="content-section">
      <view class="section-title">活动详情</view>
      <rich-text :nodes="activityInfo.content"></rich-text>
    </view>
    
    <!-- 注意事项 -->
    <view class="content-section">
      <view class="section-title">注意事项</view>
      <view class="notice-list">
        <view 
          class="notice-item"
          v-for="(item, index) in activityInfo.notices"
          :key="index"
        >
          {{index + 1}}. {{item}}
        </view>
      </view>
    </view>
    
    <!-- 底部按钮 -->
    <view class="footer" v-if="activityInfo.status === 'enrolling'">
      <button class="enroll-btn" @tap="handleEnroll">立即报名</button>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      statusText: {
        'enrolling': '报名中',
        'full': '已满员',
        'end': '已结束'
      },
      activityInfo: {
        title: '冬季禅修营',
        status: 'enrolling',
        time: '2024-01-15 ~ 2024-01-21',
        location: 'xx寺院禅修中心',
        enrollCount: 30,
        maxCount: 50,
        fee: 1000,
        image: '/static/activity/detail.jpg',
        content: `
          <div style="line-height: 1.8;">
            <p>禅修营由知名法师亲自指导，为期7天。</p>
            <p>通过禅修，可以帮助我们：</p>
            <p>1. 放松身心，减轻压力</p>
            <p>2. 提升专注力和觉知力</p>
            <p>3. 培养慈悲心和智慧</p>
          </div>
        `,
        notices: [
          '请提前15分钟到达签到',
          '请穿着宽松舒适的衣物',
          '禅修期间请保持手机静音',
          '请自备随身用品',
          '如需退订请提前3天告知'
        ]
      }
    }
  },
  onLoad(options) {
    // TODO: 根据id获取活动详情
    const { id } = options
  },
  methods: {
    handleEnroll() {
      if(this.activityInfo.enrollCount >= this.activityInfo.maxCount) {
        uni.showToast({
          title: '活动已满员',
          icon: 'none'
        })
        return
      }
      
      // TODO: 调用报名接口
      uni.showLoading({
        title: '报名中...'
      })
      
      setTimeout(() => {
        uni.hideLoading()
        uni.showToast({
          title: '报名成功',
          icon: 'success'
        })
      }, 1500)
    }
  }
}
</script>

<style lang="scss" scoped>
.activity-detail {
  min-height: 100vh;
  background: #f5f5f5;
  padding-bottom: 120rpx;
  
  .cover {
    width: 750rpx;
    height: 500rpx;
  }
  
  .info-section {
    background: #fff;
    padding: 30rpx 20rpx;
    
    .title {
      font-size: 36rpx;
      font-weight: bold;
      margin-bottom: 20rpx;
    }
    
    .status {
      display: inline-block;
      padding: 4rpx 16rpx;
      border-radius: 20rpx;
      font-size: 24rpx;
      margin-bottom: 30rpx;
      
      &.enrolling {
        background: rgba(0,255,0,0.1);
        color: #0a0;
      }
      
      &.full {
        background: rgba(255,0,0,0.1);
        color: #f00;
      }
      
      &.end {
        background: rgba(0,0,0,0.1);
        color: #666;
      }
    }
    
    .basic-info {
      .info-item {
        display: flex;
        margin-bottom: 16rpx;
        
        .label {
          width: 140rpx;
          color: #666;
          font-size: 28rpx;
        }
        
        .value {
          flex: 1;
          font-size: 28rpx;
        }
      }
    }
  }
  
  .content-section {
    background: #fff;
    margin-top: 20rpx;
    padding: 30rpx 20rpx;
    
    .section-title {
      font-size: 32rpx;
      font-weight: bold;
      margin-bottom: 20rpx;
      position: relative;
      padding-left: 20rpx;
      
      &::before {
        content: '';
        position: absolute;
        left: 0;
        top: 50%;
        transform: translateY(-50%);
        width: 6rpx;
        height: 30rpx;
        background: #f00;
        border-radius: 3rpx;
      }
    }
    
    .notice-list {
      .notice-item {
        font-size: 28rpx;
        line-height: 1.8;
        color: #666;
      }
    }
  }
  
  .footer {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    height: 100rpx;
    background: #fff;
    display: flex;
    align-items: center;
    padding: 0 20rpx;
    
    .enroll-btn {
      width: 100%;
      height: 80rpx;
      line-height: 80rpx;
      background: #f00;
      color: #fff;
      font-size: 28rpx;
      border-radius: 40rpx;
    }
  }
}
</style> 