<template>
  <view class="mine">
    <!-- 用户信息 -->
    <view class="user-info">
      <image class="bg" src="/static/mine-bg.png" mode="aspectFill"></image>
      <view class="info-content">
        <view class="avatar-box" @tap="goUserInfo">
          <image 
			v-if="userInfo.avatar"
            class="avatar" 
            :src="userInfo.avatar || '/static/mine/default-avatar.png'" 
            mode="aspectFill"
          ></image>
          <view class="name">{{userInfo.nickname || '点击登录'}}</view>
        </view>
      </view>
	  <view class="user-setting" @tap.native="goPageInfo"></view>
    </view>
	<ModulesComp :modules="modules"></ModulesComp>
	<view class="static-text static-text-bottom">永永其详，所愿必得！</view>
  </view>
</template>

<script>
import ModulesComp from '@/components/ModulesComp.vue'
const modulesList = [
  {
    name: '我的祈福许愿',
    path: '/pages/pray-order/list'
  },
  {
    name: '我的订单',
    path: '/pages/shop-order/list'
  }
]
export default {
  components:{
	ModulesComp
  },
  data() {
    return {
      userInfo: {
        avatar: '',
        nickname: ''
      },
	  modules: modulesList
    }
  },
  onShow() {
    this.getUserInfo()
  },
  methods: {
    getUserInfo() {
      // TODO: 获取用户信息
    },
    goUserInfo() {
      if(!this.userInfo.nickname) {
        uni.navigateTo({
          url: '/pages/login/index'
        })
        return
      }
    },
	goPageInfo() {
		uni.navigateTo({
			url: '/pages/userInfo/index'
		})
	}
  }
}
</script>

<style lang="scss" scoped>
.mine {
  .user-info {
    position: relative;
    height: 620upx;
    
    .bg {
      width: 100%;
      height: 380upx;
	  opacity: 0.5;
    }
    
    .info-content {
      position: absolute;
      left: 50%;
      bottom: 80upx;
	  transform: translateX(-50%);
      
      .avatar-box {
        display: flex;
        align-items: center;
		flex-direction: column;
        
        .avatar {
          width: 232upx;
          height: 232upx;
          border-radius: 50%;
          border: 2upx solid #fff;
        }
        
        .name {
          color: #101010;
          font-size: 40upx;
          margin-top: 16upx;
        }
      }
    }
	.user-setting {
	  position: absolute;
	  right: 28upx;
	  bottom: 176upx;
	  width: 48upx;
	  height: 48upx;
	  background: url('@/static/icon-setting.png') no-repeat center;
	}
  }
}
</style>
