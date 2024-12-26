<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	body {
		background-color: #fff;
		color: #333;
		font-family: PingFangSC-regular;
		font-size: 28upx;
	}
	/*每个页面公共css */
	uni-checkbox .uni-checkbox-input {
	    border-radius: 100upx; /* 设置圆角 */
	}
	button {
		margin: 0;
		padding: 0;
	}
	.btn {
	  display: inline-block;
	  padding: 20upx 40upx;
	  height: 80upx;
	  line-height: 1;
	  font-size: 32upx;
	  border-radius: 60upx;
	  box-sizing: border-box;
	}
	.btn.btn-default {
		background-color: #fff;
		color: #bd3124;
		border: 2upx solid #bd3124;
	}
	.btn.btn-primary {
		background-color: #bd3124;
		color: #fff;
	}
	.flex-center {
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.flex-start {
		display: flex;
		justify-content: flex-start;
		align-items: center;
	}
	.flex-between {
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
	.font-bold {
		font-family: PingFangSC-bold;
		font-weight: 500;
	}
	.static-text {
		line-height: 40upx;
		color: #951D1D;
		font-size: 28upx;
		text-align: center;
	}
	.static-text.static-text-bottom {
		position: fixed;
		left: 50%;
		bottom: 40upx;
		transform: translateX(-50%);
	}
	.tag {
		display: inline-block;
		padding: 0 20upx;
		height: 60upx;
		line-height: 60upx;
		border-radius: 8upx;
		color: rgba(255,255,255,1);
		font-size: 28upx;
		text-align: center;
	}
	.tag.tag-primary {
		background-color: rgba(64,149,229,1);
	}
	.tag.tag-success {
		background-color: #BD3124;
	}
	.info-list {
		padding: 0 18upx;
		font-size: 28upx;
	}
	.info-list .item {
		display: flex;
		justify-content: flex-start;
		align-items: center;
		height: 100upx;
		border-bottom: 2upx solid #f5f5f5;
	}
	.info-list .label {
		width: 128upx;
		margin-right: 18upx;
		font-size: 32upx;
		color: #101010;
	}
	.info-list .value {
		font-size: 28upx;
		color: #898989;
	}
</style>
