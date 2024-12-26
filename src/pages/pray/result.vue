<template>
  <view class="pray-result">
    <!-- 状态展示区 -->
    <view class="status status-success font-bold" v-if="status === 'success'">支付成功!</view>
    <view class="status status-fail font-bold" v-else>支付失败!</view>
    
    <template v-if="status === 'success'">
        <!-- 支付信息卡片 -->
        <view class="pay-info">
          <view class="info-item">
            <text class="value price">已收款<text class="price-value font-bold">{{ (amount / 100).toFixed(2) }}</text>元</text>
          </view>
          <view class="info-item">
            <text class="label">收款方</text>
            <text class="value">{{merchantName}}</text>
          </view>
        </view>
        
        <!-- 提示文案 -->
        <view class="tips">祈福成功后，寺庙会发送一条专属您的祈福视频！</view>
    </template>
    
    <view class="static-text">永永其详，所愿必得！</view>
    <!-- 底部按钮组 -->
    <view class="footer">
      <button class="btn btn-default" @tap="handleAgain">再祈一条</button>
      <button class="btn btn-primary" @tap="handleHome">回到首页</button>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      amount: 99,
      merchantName: '某某寺'
    }
  },
  onLoad(options) {
    // TODO: 根据订单ID获取订单信息
  },
  computed: {
    status() {
      return this.amount > 0 ? 'success' : 'fail';
    }
  },
  methods: {
    handleAgain() {
      uni.switchTab({
        url: '/pages/pray/index'
      })
    },
    handleHome() {
      uni.switchTab({
        url: '/pages/index/index'
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.pray-result {
  padding: 0 38upx;
  text-align: center;
  
  .status {
    font-size: 56upx;
    color:#333;
    margin-top: 160upx;

    &.status-fail {
        color: #bd3124;
    }
  }
  
  .pay-info {
    margin-top: 40upx;
    
    .info-item {
      margin-bottom: 60upx;
      .label {
        color: #101010;
        font-size: 32upx;
        margin-right: 30upx;
      }
      
      .value {
        font-size: 28upx;
        color: #898989;
        &.price {
          color: #333;
          font-size: 32upx;
          .price-value {
            margin: 0 10upx;
            font-size: 46upx;
          }
        }
      }
      &:last-child {
        margin-bottom: 0;
      }
    }
  }
  
  .tips {
    font-size: 32upx;
    color: #bd3124;
    margin-top: 20upx;
  }
  
  .footer {
    margin-top: 60upx;
    button:first-of-type {
      margin-right: 44upx;
    }
  }
}
.static-text {
  margin-top: 172upx;
}
</style> 