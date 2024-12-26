<template>
  <view class="login">
    <!-- Logo -->
    <view class="logo">
		<!-- 接口获取 -->
      <image src="/static/logo.png" mode="aspectFit"></image>
    </view>
    
    <!-- 隐私协议 -->
    <view class="privacy">
      <checkbox-group @change="handlePrivacyChange">
        <label>
          <checkbox class="round" :checked="isAgree" 
			color="#bbb" style="transform:scale(0.9)" activeBackgroundColor="#34CC5F"></checkbox>
          <text class="privacy-text">
            我已阅读并同意
            <text class="link" @tap.native.stop="goPrivacy">《隐私协议》</text>
          </text>
        </label>
      </checkbox-group>
    </view>
	<!-- 登录按钮 -->
	<view class="login-box">
	  <button 
	    class="wx-login-btn"
	    open-type="getUserInfo" 
	    @getuserinfo="handleGetUserInfo"
	  >
	    <text class="iconfont icon-wechat"></text>
	    <text>授权登录</text>
	  </button>
	</view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      isAgree: false
    }
  },
  methods: {
    handleGetUserInfo(e) {
      if(!this.isAgree) {
        uni.showToast({
          title: '请先同意隐私协议',
          icon: 'none'
        })
        return
      }
      
      if(e.detail.errMsg === 'getUserInfo:ok') {
        const { userInfo } = e.detail
		console.log(userInfo, 'userInfo')
        // TODO: 调用登录接口
        uni.showLoading({
          title: '登录中...'
        })
        
        setTimeout(() => {
          uni.hideLoading()
          // uni.navigateBack()
        }, 1500)
      }
    },
    handlePrivacyChange(e) {
      this.isAgree = e.detail.value.length > 0
    },
    goPrivacy() {
      uni.navigateTo({
        url: '/pages/privacy/index'
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.login {
  max-height: 100vh;
  background: #fff;
  padding: 266upx 84upx 0;
  
  .logo {
    display: flex;
    flex-direction: column;
    align-items: center;
	margin-bottom: 164upx;
    
    image {
      width: 576upx;
      height: 280upx;
	  
    }
  }
  
  .login-box {
    button {
      width: 100%;
      height: 100upx;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 32upx;
	  border-radius: 6upx;
      
      .iconfont {
        font-size: 32upx;
      }
    }
    
    .wx-login-btn {
      background: #34CC5F;
      color: #fff;
      
      &::after {
        border: none;
      }
    }
  }
  
  .privacy {
    margin-bottom: 20upx;
    
    checkbox-group {
      display: flex;
      align-items: center;
      
      label {
        display: flex;
        align-items: center;
      }
      
      .privacy-text {
        font-size: 28upx;
        color: #101010;
        margin-left: 4upx;
        
        .link {
          color: #34CC5F;
        }
      }
    }
  }
}
</style>
