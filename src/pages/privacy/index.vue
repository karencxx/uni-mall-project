<template>
  <view class="privacy">
    <!-- 标题 -->
    <view class="title">用户协议和隐私政策</view>
    
    <!-- 内容 -->
    <view class="content">
      <view class="section">
        <view class="section-title">一、总则</view>
        <view class="section-content">
          <view class="paragraph">
            1.1 本协议是您与某某寺平台（以下简称"平台"）之间关于您使用平台服务所订立的协议。
          </view>
          <view class="paragraph">
            1.2 在使用平台服务之前，请您务必仔细阅读并透彻理解本协议。
          </view>
        </view>
      </view>
      
      <view class="section">
        <view class="section-title">二、隐私保护</view>
        <view class="section-content">
          <view class="paragraph">
            2.1 我们非常重视您的个人信息保护，承诺严格按照本隐私政策所阐述的内容处理您的个人信息。
          </view>
          <view class="paragraph">
            2.2 我们收集的信息包括：
          </view>
          <view class="sub-list">
            <view class="sub-item">• 账号信息（手机号、微信账号等）</view>
            <view class="sub-item">• 个人资料（昵称、头像等）</view>
            <view class="sub-item">• 设备信息（设备型号、操作系统等）</view>
            <view class="sub-item">• 位置信息（用于推荐附近寺庙）</view>
          </view>
        </view>
      </view>
      
      <view class="section">
        <view class="section-title">三、用户行为规范</view>
        <view class="section-content">
          <view class="paragraph">
            3.1 您在使用平台服务时必须遵守中华人民共和国相关法律法规。
          </view>
          <view class="paragraph">
            3.2 您不得利用平台服务从事以下行为：
          </view>
          <view class="sub-list">
            <view class="sub-item">• 发布违法违规信息</view>
            <view class="sub-item">• 侵犯他人知识产权</view>
            <view class="sub-item">• 从事任何可能损害平台的行为</view>
          </view>
        </view>
      </view>
      
      <view class="section">
        <view class="section-title">四、其他条款</view>
        <view class="section-content">
          <view class="paragraph">
            4.1 平台保留随时修改本协议的权利，修改后的协议将在平台上公布。
          </view>
          <view class="paragraph">
            4.2 本协议的解释权归平台所有。
          </view>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {}
  }
}
</script>

<style lang="scss" scoped>
.privacy {
  min-height: 100vh;
  background: #fff;
  padding: 40rpx;
  
  .title {
    font-size: 40rpx;
    font-weight: bold;
    text-align: center;
    margin-bottom: 60rpx;
  }
  
  .content {
    .section {
      margin-bottom: 40rpx;
      
      .section-title {
        font-size: 32rpx;
        font-weight: bold;
        margin-bottom: 20rpx;
      }
      
      .section-content {
        .paragraph {
          font-size: 28rpx;
          color: #333;
          line-height: 1.8;
          margin-bottom: 20rpx;
        }
        
        .sub-list {
          padding-left: 20rpx;
          
          .sub-item {
            font-size: 28rpx;
            color: #666;
            line-height: 1.8;
          }
        }
      }
    }
  }
}
</style> 