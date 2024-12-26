<template>
  <view class="pray-order">
    <!-- 商品信息 -->
    <view class="goods-info">
      <image :src="goodsInfo.image" mode="aspectFill"></image>
      <view class="info">
        <view class="sku">{{goodsInfo.skuName}}</view>
        <view class="num">{{ `¥ ${ price } * ${goodsInfo.num}`}} </view>
        <view class="price font-bold">¥{{ price }}</view>
      </view>
    </view>
    
    <!-- 表单区域 -->
    <view class="form-content"> 
      <!-- 祈福者 -->
      <view class="form-item">
        <view class="label">祈福者</view>
        <input 
          type="text"
          v-model="form.name"
          placeholder="请输入祈福者姓名"
          placeholder-class="placeholder"
        />
		<text>请输入真实姓名</text>
      </view>
      
      <!-- 祈福类型 -->
      <view class="form-item">
        <view class="label">祈福类型</view>
        <picker 
          @change="bindPickerChange" 
          :value="form.typeIndex" 
          :range="prayTypes"
          range-key="name"
		  class="picker"
        >
            {{prayTypes[form.typeIndex]&&prayTypes[form.typeIndex].name || '请选择祈福类型'}}
        </picker>
      </view>
      
      <!-- 祈福祝语 -->
      <view class="form-item">
        <view class="label">祈福祝语</view>
		<input
		  type="text"
		  v-model="form.wish"
		  placeholder="请输入祈福祝语"
		  placeholder-class="placeholder"
          maxlength="16"
		/>
		<text>限16字</text>
      </view>
    </view> 
    
    <view class="static-text">永永其详，所愿必得！</view>
    <!-- 底部按钮 -->
    <view class="footer flex-center">
      <button class="btn btn-default" @tap="back">再祈一条</button>
      <button class="btn btn-primary" @tap="handleSubmit">立即祈福</button>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      goodsInfo: {
        image: '/static/logo.png',
        title: '丝带祈福',
        skuName: '平安祈福',
        price: 2000,
        num: 1
      },
      prayTypes: [
        { id: 1, name: '消灾祈福' },
        { id: 2, name: '升学祈福' },
        { id: 3, name: '姻缘祈福' },
        { id: 4, name: '事业祈福' },
        { id: 5, name: '健康祈福' }
      ],
      form: {
        name: '花三肥四',
        typeIndex: 1,
        wish: '注入诸如'
      }
    }
  },
  onLoad(options) {
    // TODO: 根据skuId获取商品信息
    const { skuId, num } = options
  },
  computed: {
    price() {
      return (this.goodsInfo.price / 100).toFixed(2)
    }
  },
  methods: {
    bindPickerChange(e) {
      this.form.typeIndex = e.detail.value
    },
    back() {
      uni.navigateBack()
    },
    handleSubmit() {
      if(!this.form.name) {
        uni.showToast({
          title: '请输入祈福者姓名',
          icon: 'none'
        })
        return
      }
      
      if(this.form.typeIndex === -1) {
        uni.showToast({
          title: '请选择祈福类型',
          icon: 'none'
        })
        return
      }
      
      if(!this.form.wish) {
        uni.showToast({
          title: '请输入祈福祝语',
          icon: 'none'
        })
        return
      }
      
      // TODO: 提交订单
      uni.navigateTo({
        url: '/pages/pray/confirm?skuId=' + this.goodsInfo.skuId + '&num=' + this.goodsInfo.num
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.placeholder {
    color: #101010;
}
.pray-order {
    padding: 52upx 40upx;
    .goods-info {
        display: flex;
        align-items: center;
        margin-bottom: 80upx;
        font-size: 28upx;

        image {
            width: 80upx;
            height: 80upx;
        }
        .info {
            display: flex;
            justify-content: space-between;
            flex: 1;
            margin-left: 16upx;
            
            .sku {
                color: #6c6c6c;
            }
            .num, .price {
                color: #bd3124;
            }
            .price {
                font-size: 32upx;
            }
        }
    }
    .form-content {
        .form-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            height: 100upx;
            font-size: 28upx;
            color: #101010;
            border-bottom: 2upx solid #f5f5f5;
            
            .label {
                flex: 0 0 128upx;
                font-size: 32upx;
                margin-right: 20upx;
            }
            
            input {
                flex: 1;
                padding-right: 12upx;
            }
            
            .picker {
                flex: 1;
                color: #101010;
            }
        }
    }
    .footer {
        margin-top: 100upx;

        button:first-of-type {
            margin-right: 80upx;
        }
    }
}
.static-text {
    margin-top: 48upx;
}
</style>
