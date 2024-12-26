<template>
  <view class="pray-order-list">
    
    <!-- 类型筛选 -->
    <view class="search-bar flex-start">
        <uni-data-select
            class="search-select"
            v-model="currentTab"
            :localdata="tabs"
            @change="switchTab"
            :clear="false"></uni-data-select>
        <view class="search-input">
            <view class="search-area">
                <uni-icons type="search" size="16" color="#666"></uni-icons>
                <input 
                  type="text"
                  v-model.trim="searchKey"
                  placeholder="搜索"
                  placeholder-class="placeholder"/>
            </view>
          <text>搜索</text>
        </view>
    </view>
    
    <!-- 订单列表 -->
    <view class="order-list info-list">
      <view 
        class="order-item"
        v-for="(item, index) in orderList" 
        :key="index"
        @tap="goDetail(item)"
      >
          <text class="type">{{item.typeName}}</text>
          <text class="date">{{item.createTime}}</text>
          <text class="num">{{item.num}}份</text>
          <text class="status" :class="item.status">{{item.statusText}}</text>
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
          text: '待祈福'
        },
        {
          value: 2,
          text: '已祈福'
        }
      ],
      orderList: [
        {
          id: 1,
          typeName: '丝带祈福',
          name: '张三',
          createTime: '2024-01-01',
          num: 1,
          status: 'pending',
          statusText: '待祈福'
        },
        {
          id: 2,
          typeName: '福牌祈福',
          name: '李四',
          createTime: '2024-01-02',
          num: 2,
          status: 'finished',
          statusText: '已祈福'
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
        url: `/pages/pray-order/detail?id=${item.id}`
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.pray-order-list {
  
  .search-bar {
    padding: 20upx 20upx 40upx;

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
    padding: 0 18upx;
    
    .order-item {
      display: flex;
      align-items: center;
      justify-content: space-between;
      font-size: 28upx;
      height: 100upx;
      border-bottom: 2upx solid #f5f5f5;
        
        .type {
          font-size: 32upx;
          color: #101010;
          margin-left: 30upx;
        }
        .date {
          color: #898989;
        }
        .num {
          color: #bd3124;
        }
        
        .status {
          width: 160upx;
          height: 60upx;
          margin-right: 16upx;
          font-size: 28upx;
          border: 2upx solid #3ab54b;
          color: #3ab54b;
          text-align: center;
          line-height: 60upx;
          border-radius: 8upx;
        }
    }
  }
}

.placeholder {
  color: #bdbdbd;
}
</style> 