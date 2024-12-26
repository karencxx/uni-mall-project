<template>
  <view class="pray-confirm">
    <!-- 订单信息卡片 -->
    <view class="order-info">
      <view class="info-item">
        <text class="tag">{{orderInfo.typeName}}</text>
      </view>
      <view class="info-item">
        <text class="label">祈福者</text>
        <text class="value">{{orderInfo.name}}</text>
      </view>
      <view class="info-item">
        <text class="label">祈福类型</text>
        <text class="value type">{{orderInfo.name}}</text>
      </view>
      <view class="info-item">
        <text class="label">祈福祝语</text>
        <text class="value">{{orderInfo.wish}}</text>
      </view>
    </view>
    <view class="static-text">永永其详，所愿必得！</view>
    
    <view class="footer">
      <view class="pay-amount">
       共<text class="amount">{{ (orderInfo.amount / 100).toFixed(2) }}</text>元
      </view>
      <button class="btn btn-primary" @tap.native="handlePay">立即支付</button>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      orderInfo: {
        typeName: '平安祈福',
        name: '张三',
        type: '求财',
        wish: '愿一切平安顺遂',
        amount: 990
      }
    }
  },
  onLoad(options) {
    // TODO: 根据订单ID获取订单信息
  },
  methods: {
    handlePay() {
      // TODO: 调用支付接口
      uni.showLoading({
        title: '支付中...'
      })
      
      setTimeout(() => {
        uni.hideLoading()
        uni.redirectTo({
          url: '/pages/pray/result?status=success'
        })
      }, 1500)
    }
  }
}
</script>

<style lang="scss" scoped>
.pray-confirm {
  padding: 44upx 18upx;
  
  .order-info {
    color: #101010;
    
    .info-item {
      display: flex;
      align-items: center;
      height: 100upx;
      border-bottom: 2upx solid #f5f5f5;

      &:first-child {
        border: none;
      }
      
      .label {
        width: 128upx;
        font-size: 32upx;
        margin-left: 30upx;
      }
      
      .tag {
        margin-left: 16upx;
        padding: 0 24upx;
        height: 60upx;
        line-height: 60upx;
        border-radius: 8upx;
        background-color: rgba(189,49,36,1);
        color: rgba(255,255,255,1);
        font-size: 28upx;
        text-align: center;
      }
      .value {
        flex: 1;
        margin-left: 20upx;
        font-size: 28upx;
        color: #898989;
        &.type {
          color: #101010;
        }
      }
    }
  }
  
  .footer {
    text-align: center;
    margin-top: 100upx;
    .pay-amount {
      font-size: 32upx;
      color: #951d1d;
      line-height: 80upx;
      
      .amount {
        font-size: 46upx;
        font-weight: bold;
        margin: 6upx;
      }
    }
    .btn {
      margin: 0 auto;
      width: max-content;
    }
  }
}
.static-text {
  margin-top: 48upx;
}
</style> 