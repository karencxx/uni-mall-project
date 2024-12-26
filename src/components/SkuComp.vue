<template>
	<view>
		<uni-popup ref="skuPopup" type="bottom">
		  <view class="sku-popup">
		    <view class="header">
		      <image :src="goodsInfo.image" mode="aspectFill"></image>
		      <view class="info">
		        <view class="price font-bold">¥{{goodsInfo.price}}</view>
		        <!-- <view class="selected">已选：{{selectedSku ? selectedSku.name : '请选择款式'}}</view> -->
		        <view class="stock">剩余 10000</view>
		      </view>
		      <view class="close" @tap.native.stop="closeSkuPopup"><uni-icons type="closeempty" size="22" color="#4f4f4f"></uni-icons></view>
			</view>
			<slot name="release"></slot>
		    
		    <view class="content">
		      <!-- 款式选择 -->
		      <view class="sku-group">
		        <view class="label">请选择款式</view>
		        <view class="options">
		          <view 
		            class="option-item" 
		            :class="{active: selectedSku&&selectedSku.id === item.id}"
		            v-for="item in skuList" 
		            :key="item.id"
		            @tap="selectSku(item)"
		          >
		            <image :src="item.image" mode="widthFix" v-if="item.image"></image>
		            <uni-icons type="spinner-cycle" size="22" color="#4f4f4f" v-else></uni-icons>
		            <view>
						<text>{{item.name}}</text>
						<text class="price font-bold">¥ {{(item.price/100).toFixed(2)}}</text>
					</view>
		          </view>
		        </view>
		      </view>
		      
		      <!-- 数量选择 -->
		      <view class="number">
		        <view class="label">数量</view>
		        <uni-number-box
				  class="custom-number-box"
		          v-model.number="buyNum"
		          :min="1"
		          :max="99"
				  width="56"
				  background="#fff"
				  color="#101010"
		        ></uni-number-box>
		      </view>
		    </view>
		    
		    <view class="footer">
		      <button class="confirm-btn" @tap.native.stop="handleConfirm">立即祈福</button>
		    </view>
		  </view>
		</uni-popup>
	</view>
</template>

<script>
export default {
  props: {
    goodsInfo: {
      type: Object,
      default: () => ({})
    },
    skuList: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      selectedSku: null,
      buyNum: 1
    }
  },
  methods: {
    open() {
      this.$refs.skuPopup.open()
    },
    close() {
      this.$refs.skuPopup.close()
    },
    closeSkuPopup() {
      this.close()
    },
    selectSku(sku) {
      if (this.selectedSku === sku) {
        this.selectedSku = null
      } else {
        this.selectedSku = sku
      }
    },
    handleConfirm() {
      if(!this.selectedSku) {
        uni.showToast({
          title: '请选择款式',
          icon: 'none'
        })
        return
      }
      this.$emit('confirm', {
        sku: this.selectedSku,
        num: this.buyNum
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.sku-popup {
  background: #fff;
  border-radius: 60upx 60upx 0 0;
  
  .header {
    display: flex;
    padding: 36upx 44upx;
    
    image {
      width: 124upx;
      height: 124upx;
    }
    
    .info {
      flex: 1;
      padding: 0 16upx;
      
      .price {
        color: #e99d42;
        font-size: 36upx;
        margin-bottom: 12upx;
      }
	  .stock {
		  color: #6c6c6c;
		  font-size: 28upx;
	  }
    }
  }
  
  .content {
    padding: 30upx 40upx;
    
    .sku-group {
      margin-bottom: 40upx;
      font-size: 28upx;
      color: #6c6c6c;
      
      .label {
        margin-bottom: 28upx;
      }
      
      .options {
        display: flex;
        flex-wrap: wrap;
		gap: 36upx;
        
        .option-item {
		  display: flex;
		  align-items: center;
		  flex: 0 0 188upx;
          font-size: 28upx;
          color: #6c6c6c;
          
          &.active {
            border: 2upx solid #E99D42;
			transform: scale(1.2);
          }
		  image {
			  width: 80upx;
			  height: 80upx;
			  margin-right: 4upx;
		  }
		  .price {
			  display: inline-block;
			  color: #E99D42;
		  }
        }
      }
    }
    
    .number {
		display: flex;
		justify-content: space-between;
		align-items: center;
		.label {
			font-size: 28upx;
			color: #101010;
		}
    }
  }
  
  .footer {
    padding: 20upx;
    
    .confirm-btn {
      height: 100upx;
      line-height: 100upx;
      background: #e99d42;
      color: #fff;
      font-size: 32upx;
      border-radius: 40upx;
    }
  }
}

	
	.custom-number-box {
		height: 60upx;
		// font-size: 28upx;
		border: 2upx solid #bbb;
		border-radius: 4upx;
	}

</style>