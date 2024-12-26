<template>
	<view class="barrage">
		<view class="barrage-row" v-for="(row, rowIndex) in 3" :key="rowIndex">
			<view v-for="(item, index) in getRowItems(rowIndex)" :key="index">
				<view class="barrage-item" >
					<!-- :style="getItemStyle(rowIndex, index)" -->
					<image src="@/static/icons/icon-danmu.png" mode="aspectFill"></image>
					<text>{{item}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name:"Barrage",
		props: {
			list: {
				type: Array,
				default: () => []
			}
		},
		data() {
			return {
				rowData: [[], [], []], // 三行数据
				startTimes: [0, 0, 0], // 每行开始时间
			}
		},
		mounted() {
			this.initBarrage()
		},
		methods: {
			initBarrage() {
				// 随机分配数据到三行
				const shuffled = [...this.list].sort(() => 0.5 - Math.random())
				this.rowData = [
					shuffled.slice(0, Math.floor(shuffled.length/3)),
					shuffled.slice(Math.floor(shuffled.length/3), Math.floor(shuffled.length*2/3)),
					shuffled.slice(Math.floor(shuffled.length*2/3))
				]
				
				// 每行随机起始时间
				this.startTimes = this.rowData.map(() => Math.random() * 5)
			},
			getRowItems(rowIndex) {
				return this.rowData[rowIndex] || []
			},
			getItemStyle(rowIndex, index) {
				const delay = this.startTimes[rowIndex] + index * 3 // 每条弹幕间隔3秒
				return {
					animationDelay: `${delay}s`,
					animationDuration: '8s'
				}
			}
		},
		watch: {
			list: {
				handler(newVal) {
					if(newVal.length > 0) {
						this.initBarrage()
					}
				},
				immediate: true
			}
		}
	}
</script>

<style lang="scss">
.barrage {
	width: 100%;
	display: flex;
	flex-direction: column;
	gap: 18upx;
	position: absolute;
	top: 8upx;
	left: 0;
	height: 260upx;
	overflow: hidden;
	z-index: 1;
	
	.barrage-row {
		position: relative;
		height: 72upx;
		overflow: hidden;
		
		.barrage-item {
			position: absolute;
			right: 0;
			display: flex;
			justify-content: flex-end;
			align-items: center;
			animation: barrage 8s linear infinite;
			
			image {
				width: 56upx;
				height: 60upx;
				z-index: 1;
			}
			
			text {
				margin-left: -28upx;
				padding: 0 40upx;
				height: 72upx;
				line-height: 72upx;
				color: #951d1d;
				font-size: 28upx;
				border: 2upx solid #F4CE98;
				background-color: rgba(255,255,255,0.5);
				border-radius: 32upx;
				box-sizing: border-box;
			}
		}
	}
}

@keyframes barrage {
	from {
		transform: translateX(101%);
	}
	to {
		transform: translateX(-100%);
	}
}
</style>