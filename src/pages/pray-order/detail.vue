<template>
  <view class="pray-order-detail">
    <!-- 状态展示 -->
    <view class="status tag" :class="statusClassNm">{{orderInfo.statusText}}</view>
    
    <!-- 订单信息 -->
    <view class="info-list">
      <view class="item">
        <text class="label">祈福者</text>
        <text class="value">{{orderInfo.name}}</text>
      </view>
      <view class="item">
        <text class="label">祈福类型</text>
        <text class="value type">{{orderInfo.typeName}}</text>
      </view>
      <view class="item">
        <text class="label">祈福祝语</text>
        <text class="value">{{orderInfo.wish}}</text>
      </view>
      <view class="item">
        <text class="label">祈福时间</text>
        <text class="value">{{orderInfo.createTime}}</text>
      </view>
    </view>
    <view class="static-text">永永其详，所愿必得！</view>

    <!-- 祈福视频 -->
    <view class="video-card">
      <template v-if="orderInfo.videoUrl">
        <video :src="orderInfo.videoUrl"></video>
        <view class="video-text">请查看祈福视频</view>
      </template>
      <template v-else>
        <view class="empty"></view>
        <view class="empty-text">敬请期待祈福视频</view>
      </template>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      orderInfo: {
        id: 1,
        typeName: '丝带祈福',
        name: '张三',
        wish: '愿一切平安顺遂',
        createTime: '2024-01-01 12:00:00',
        status: 'success',
        statusText: '已祈福',
        videoUrl: ''
      },
      statusClassNm: 'tag-primary'
    }
  },
  onLoad(options) {
    // TODO: 根据id获取订单详情
    const { id } = options
    this.statusClassNm = this.orderInfo.status === 'pending' ? 'tag-primary' : 'tag-success'
  }
}
</script>

<style lang="scss" scoped>
.pray-order-detail {
    position: relative;
    padding-top: 56upx;
    .status {
        position: absolute;
        top: 40upx;
        right: 40upx;
    }

  .info-list {
    .value.type {
      color: #101010;
    }
  }
  .video-card {
    padding: 68upx 0 ;
    width: 568upx;
    margin: 0 auto;

    video {
      width: 100%;
      height: 548upx;
    }
    
    .empty {
      height: 548upx;
      background-color: #efefef;
      background-image: url('@/static/icons/icon-video.png');
      background-size: 50% 50%;
      background-repeat: no-repeat;
      background-position: center;
    }
    .empty-text, .video-text {
      font-size: 28upx;
      color: #4f4f4f;
      text-align: center;
      margin-top: 40upx;
    }
  }
}
.static-text {
    margin-top: 64upx;
}
</style> 