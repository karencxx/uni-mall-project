<template>
  <view class="user-info">
    <!-- 基本信息 -->
    <view class="info-list">
      <!-- 头像 -->
      <view class="info-item">
        <text class="label">用户头像</text>
        <view class="value avatar-box">
          <image
			v-if="userInfo.avatar"
            class="avatar" 
            :src="userInfo.avatar" 
            mode="aspectFill"
          ></image>
		  <uni-icons v-else type="image-filled" size="30"></uni-icons>
        </view>
      </view>
      
      <!-- 昵称 -->
      <view class="info-item">
        <text class="label">用户昵称</text>
        <view class="value">
          <text>{{userInfo.nickname || '未设置'}}</text>
        </view>
      </view>
	  
	  <!-- 收货地址 -->
      <view class="info-item">
        <text class="label">收货地址</text>
        <view class="value">
          <text>{{userInfo.address || '未设置'}}</text>
		   <uni-icons type="right" size="30"></uni-icons>
        </view>
      </view>
      
      <!-- 手机号 -->
      <view class="info-item">
        <text class="label">手机号</text>
        <view class="value phone-box">
          <text>{{userInfo.phone ? formatPhone(userInfo.phone) : '未绑定'}}</text>
          <button class="phone-btn" open-type="getPhoneNumber" @getphonenumber="getPhoneNumber">微信授权</button>
        </view>
      </view>
    </view>
    <view class="static-text static-text-bottom">永永其详，所愿必得！</view>
    <!-- 退出登录 -->
    <!-- <button class="logout-btn" @tap="handleLogout">退出登录</button> -->
  </view>
</template>

<script>
export default {
  data() {
    return {
      userInfo: {
        avatar: '',
        nickname: '',
        phone: ''
      }
    }
  },
  onShow() {
    this.getUserInfo()
  },
  methods: {
    getUserInfo() {
      // TODO: 获取用户信息
    },
    formatPhone(phone) {
      return phone.replace(/(\d{3})\d{4}(\d{4})/, '$1****$2')
    },
    // chooseAvatar() {
    //   uni.chooseImage({
    //     count: 1,
    //     sizeType: ['compressed'],
    //     sourceType: ['album', 'camera'],
    //     success: (res) => {
    //       const tempFilePath = res.tempFilePaths[0]
    //       // TODO: 上传头像
    //       uni.showLoading({
    //         title: '上传中...'
    //       })
          
    //       setTimeout(() => {
    //         uni.hideLoading()
    //         this.userInfo.avatar = tempFilePath
    //         uni.showToast({
    //           title: '上传成功',
    //           icon: 'success'
    //         })
    //       }, 1500)
    //     }
    //   })
    // },
	getPhoneNumber(event) {
		console.log(event)
	  if (event.detail.errMsg == 'getPhoneNumber:ok') {
		// 获取 encryptedData 与 iv 传给后台进行解析
		console.log(event.detail);
		// 这里可以发送请求到你的后端服务器，携带 encryptedData 和 iv
		// 后端需要使用 session_key 解密获取用户手机号
	  } else {
		// 处理用户拒绝授权的情况
		console.log('用户拒绝授权');
	  }
	},
    // bindPhone() {
    //   if(this.userInfo.phone) {
    //     uni.showToast({
    //       title: '手机号已绑定',
    //       icon: 'none'
    //     })
    //     return
    //   }
    //   uni.navigateTo({
    //     url: '/pages/login/phone'
    //   })
    // },
    // handleLogout() {
    //   uni.showModal({
    //     title: '提示',
    //     content: '确定要退出登录吗？',
    //     success: (res) => {
    //       if(res.confirm) {
    //         // TODO: 调用退出登录接口
    //         uni.showLoading({
    //           title: '退出中...'
    //         })
            
    //         setTimeout(() => {
    //           uni.hideLoading()
    //           uni.reLaunch({
    //             url: '/pages/index/index'
    //           })
    //         }, 1500)
    //       }
    //     }
    //   })
    // }
  }
}
</script>

<style lang="scss" scoped>
.user-info {
  padding: 60upx 20upx;
  
  .info-list {
    
    .info-item {
      display: flex;
      justify-content: flex-start;
      align-items: center;
	  height: 100upx;
      padding: 0 30upx;
      border-bottom: 2upx solid #F5F5F5;
	  box-sizing: border-box;
      
      .label {
        font-size: 32upx;
		line-height: 44upx;
		color: #101010;
      }
      
      .value {
        display: flex;
		flex: 1;
        align-items: center;
		margin-left: 16upx;
        
        text {
			display: inline-block;
			color: #898989;
			font-size: 28upx;
        }
        
        .icon-right {
          color: #999;
          margin-left: 10upx;
        }
      }
      
      .avatar-box {
		  justify-content: flex-end;
        .avatar {
          width: 144upx;
          height: 88upx;
          border-radius: 2upx;
        }
      }
	  
	  .phone-box {
		  justify-content: space-between;
		  
		  .phone-btn {
			  width: 160upx;
			  height: 60upx;
			  margin: 0;
			  padding: 0;
			  line-height: 60upx;
			  color: #3AB54B;
			  font-size: 28upx;
			  text-align: center;
			  background-color: rgba(255,255,255,1);
			  border: 2upx solid #3AB54B;
			  border-radius: 8upx;
		  }
	  }
    }
  }
  
  // .logout-btn {
  //   width: 710rpx;
  //   height: 88rpx;
  //   line-height: 88rpx;
  //   background: #fff;
  //   color: #f00;
  //   font-size: 32rpx;
  //   border-radius: 12rpx;
  //   margin: 40rpx auto;
    
  //   &::after {
  //     border: none;
  //   }
  // }
}
</style> 