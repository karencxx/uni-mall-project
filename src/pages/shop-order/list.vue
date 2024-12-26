<template>
  <view class="shop-order-list">
    <!-- 搜索栏 -->
    <view class="search-bar flex-start">
      <uni-data-select
        class="search-select"
        v-model="currentTab"
        :localdata="tabs"
        @change="switchTab"
        :clear="false"
      ></uni-data-select>
      <view class="search-input">
        <view class="search-area">
          <uni-icons type="search" size="16" color="#666"></uni-icons>
          <input 
            type="text"
            v-model.trim="searchKey"
            placeholder="搜索"
            placeholder-class="placeholder"
          />
        </view>
        <text>搜索</text>
      </view>
    </view>
    
    <!-- 订单列表 -->
    <view class="order-list">
      <view 
        class="order-item"
        v-for="(item, index) in orderList" 
        :key="index"
        @tap="goDetail(item)"
      >
        <view class="header">
          <view class="order-no"><text class="label">订单号</text>{{item.orderNo}}</view>
          <text class="status tag" :class="item.status === 'pending' ? 'tag-primary' : 'tag-success'">{{item.statusText}}</text>
        </view>
        <view class="goods-info flex-start">
          <image :src="item.image" mode="aspectFill"></image>
          <view class="info">
            <view class="info-row1">
                <text class="title">{{item.title}}</text>
                <view>
                    <text class="price">¥{{(item.price/100).toFixed(2)}}</text>
                    <text class="num">x{{item.num}}</text>
                </view>
                <text class="total font-bold">¥ {{(item.totalAmount/100).toFixed(2)}}</text>
            </view>
            <view class="info-row2">
                <text class="time">{{item.createTime}}</text>
            </view>
          </view>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      searchKey: '',
      currentTab: 0,
      tabs: [
        {
          value: 0,
          text: '全部'
        },
        {
          value: 1,
          text: '待付款'
        },
        {
          value: 2,
          text: '待发货'
        },
        {
          value: 3,
          text: '待收货'
        },
        {
          value: 4,
          text: '已完成'
        }
      ],
      orderList: [
        {
          id: 1,
          orderNo: 'DD202401010001',
          title: '佛珠手链',
          image: '/static/shop/goods1.png',
          price: 9900,
          num: 1,
          totalAmount: 9900,
          createTime: '2024-01-01',
          status: 'pending',
          statusText: '待签收'
        },
        {
          id: 2,
          orderNo: 'DD202401010002',
          title: '平安符',
          image: '/static/shop/goods2.png',
          price: 2900,
          num: 2,
          totalAmount: 5800,
          createTime: '2024-01-02',
          status: 'shipped',
          statusText: '待收货'
        }
      ]
    }
  },
  methods: {
    switchTab(index) {
      this.currentTab = index
      // TODO: 根据状态筛选订单
    },
    goDetail(item) {
      uni.navigateTo({
        url: `/pages/shop-order/detail?id=${item.id}`
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.shop-order-list {
  .search-bar {
    padding: 20upx 20upx 32upx;

    .search-select {
      width: 176upx;
      height: 60upx;
    }
    
    .search-input {
      flex: 1;
      display: flex;
      align-items: center;
      margin-left: 24upx;
      height: 72upx;
      background: #e8e8e8;
      padding: 16upx;

      .search-area {
        display: flex;
        align-items: center;
        flex: 1;
        background: #fff;
      }
      
      input {
        flex: 1;
        height: 100%;
        font-size: 28upx;
      }
    }
  }
  
  .order-list {
    
    .order-item {
      margin: 0 20upx;
      .header {
          display: flex;
          justify-content: space-between;
          align-items: center;
          height: 80upx;
          padding: 0 30upx;
        
        .order-no {
          font-size: 28upx;
          color: #898989;

          .label {
            margin-right: 50upx;
            color: #101010;
            font-size: 32upx;
          }
        }
      }
      
      .goods-info {
        padding: 24upx;
        border-top: 2upx solid #f5f5f5;
        border-bottom: 2upx solid #f5f5f5;
        image {
          width: 96upx;
          height: 120upx;
          background: #e5e5e5;
        }
        
        .info { 
          margin-left: 20upx;
          flex: 1;
          align-self: flex-end;
          .info-row1 {
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 32upx;
            color: #bd3124;

            .title {
              color: #101010;
            }
            .price {
                margin-right: 20upx;
            }
          }
          .info-row2 {
            color: #898989;
            font-size: 26upx;
            text-align: right;
          }
        }
      }
      
    }
  }
}

.placeholder {
  color: #bdbdbd;
}
</style>
