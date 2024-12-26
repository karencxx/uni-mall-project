<template>
  <view class="shop-order-detail">
    <!-- 商品信息 -->
    <view class="goods-card common-card">
        <view class="title flex-between">
            <text class="label">订单号：{{orderInfo.orderNo}}</text>
            <text class="status tag" :class="orderInfo.status === 'pending' ? 'tag-primary' : 'tag-success'">{{orderInfo.statusText}}</text>
        </view>

        <view class="goods-info" v-for="(item, index) in orderInfo.goodslists" :key="index">
            <image :src="item.image" mode="aspectFill"></image>
            <view class="info">
                <view class="info-title font-bold">{{item.title}}</view>
                <view class="price-sku">
                    <text class="sku">{{item.sku}}</text>
                    <text class="price">¥{{(item.price/100).toFixed(2)}}</text>
                </view>
                <view class="num">数量：{{item.num}}</view>
            </view>
        </view>
        <view class="amount-info">  
            实付款：¥{{((orderInfo.totalAmount + orderInfo.expressAmount)/100).toFixed(2)}}
        </view>
        <view class="title flex-between no-border">
            <text class="label">订单备注</text>
            <text class="value">{{ orderInfo.remark }}</text>
        </view>
    </view>
    <view class="express-card common-card" v-if="orderInfo.express">
        <view class="title">物流配送</view>
        <view class="express-info">
                w
        </view>
        <view class="address-info">
                <view class="user">{{orderInfo.address.name}} {{orderInfo.address.phone}}</view>
                <view class="address">{{orderInfo.address.address}}</view>
        </view>
    </view>
    
    <!-- 订单信息 -->
    <view class=" common-card">
      <view class="title">更多信息</view>
      <view class="info-item">
        <text class="label">订单编号</text>
        <text class="value">{{orderInfo.orderNo}}</text>
      </view>
      <view class="info-item">
        <text class="label">下单时间</text>
        <text class="value">{{orderInfo.createTime}}</text>
      </view>
      <view class="info-item" v-if="orderInfo.payTime">
        <text class="label">支付时间</text>
        <text class="value">{{orderInfo.payTime}}</text>
      </view>
      <view class="info-item" v-if="orderInfo.shipTime">
        <text class="label">发货时间</text>
        <text class="value">{{orderInfo.shipTime}}</text>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      orderInfo: {
        id: 1,
        orderNo: 'DD202401010001',
        title: '佛珠手链',
        image: '/static/shop/goods1.png',
        price: 9900,
        num: 1,
        totalAmount: 9900,
        expressAmount: 1000,
        createTime: '2024-01-01 12:00:00',
        payTime: '2024-01-01 12:01:00',
        shipTime: '2024-01-02 12:00:00',
        status: 'shipped',
        statusText: '待收货',
        statusDesc: '商品已发出，请注意查收',
        express: {
          company: '顺丰快递',
          no: 'SF1234567890'
        },
        address: {
          name: '张三',
          phone: '138****8888',
          address: '浙江省杭州市西湖区xxx路xxx号'
        },
        goodslists: [
            {
                sku: '规格：108颗',
                title: '佛珠手链',
                image: '/static/shop/goods1.png',
                price: 9900,
                num: 1
            },
            {
                sku: '规格：10颗',
                title: '佛珠手链',
                image: '/static/logo.png',
                price: 980,
                num: 1,
            }
        ],
        remark: '请尽快发货'
      }
    }
  },
  onLoad(options) {
    // TODO: 根据id获取订单详情
    const { id } = options
  }
}
</script>

<style lang="scss" scoped>
.shop-order-detail {
  min-height: 100vh;
  background: #fff;
  padding: 24upx;
  
  .common-card {
    background: #efefef;
    border-radius: 12upx;
    padding: 0 16upx;
    font-size: 28upx;
    color: #4f4f4f;
    margin-bottom: 24upx;å

    .title {
        font-size: 32upx;
        line-height: 44upx;
        padding: 12upx 0 12upx 32upx;
        border-bottom: 2upx solid #bbbbbb;

        &.no-border {
            border-bottom: none;
        }
    }

    .info-item {
        padding: 16upx 32upx 0;
        display: flex;
        justify-content: space-between;
        align-items: center;

        &:last-child {
            padding-bottom: 16upx;
        }
    }
  }
  
  .express-card {
    
    .express-info {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding-bottom: 30upx;
      border-bottom: 1upx solid #eee;
      
      .left {
        display: flex;
        align-items: center;
        
        image {
          width: 80upx;
          height: 80upx;
        }
        
        .info {
          margin-left: 20upx;
          
          .company {
            font-size: 28upx;
            color: #333;
            margin-bottom: 8upx;
          }
          
          .no {
            font-size: 24upx;
            color: #666;
          }
        }
      }
    }
    
    .address-info {
      padding-top: 30upx;
      
      .label {
        font-size: 28upx;
        color: #666;
        margin-bottom: 16upx;
      }
      
      .value {
        .user {
          font-size: 28upx;
          color: #333;
          margin-bottom: 8upx;
        }
        
        .address {
          font-size: 28upx;
          color: #666;
        }
      }
    }
  }
  
  .goods-card {
    .title {
        .label {
            color: #101010;
        }
    }
    .goods-info {
      display: flex;
      padding: 30upx 28upx 20upx;
      border-bottom: 2upx solid #bbb;
      
      image {
        width: 144upx;
        height: 144upx;
      }
      
      .info {
        flex: 1;
        margin-left: 24upx;
        color: #101010;
        font-size: 28upx;
        
        .info-title {
            margin-bottom: 6upx;
            font-size: 32upx;
            font-family: PingFangSC-bold;
        }
        
        .price-sku {
            margin-bottom: 6upx;
          .price {
            color: #e99d42;
          }
          .sku {
            margin-right: 24upx;
            color: #6c6c6c;
          }
        }
      }
    }
    
    .amount-info {
      padding-top: 30upx;
      
      .item {
        display: flex;
        justify-content: space-between;
        margin-bottom: 16upx;
        
        &:last-child {
          margin-bottom: 0;
        }
        
        &.total {
          padding-top: 16upx;
          border-top: 1upx solid #eee;
          
          .label, .value {
            color: #333;
            font-weight: bold;
          }
        }
        
        .label {
          font-size: 28upx;
          color: #666;
        }
        
        .value {
          font-size: 28upx;
          color: #333;
        }
      }
    }
  }
}
</style>
