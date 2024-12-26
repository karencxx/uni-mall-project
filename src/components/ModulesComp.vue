<template>
    <view class="comp-container">
        <view class="module flex-center" v-for="(module, index) in modules" :key="index" @tap.native="navigateTo(module)">
            <image v-if="module.icon" :src="module.icon" mode="aspectFit"></image>
            <text>{{ module.name }}</text>
        </view>
    </view>
</template>
<script>
export default {
    name: 'ModulesComp',
    props: {
        modules: {
            type: Array,
            default: []
        },
        // 一行显示的模块数
        rowNum: {
            type: Number,
            default: 2
        }
    },
    methods: {
        navigateTo(module) {
			const { path, navigateTo } = module
			if(navigateTo === 'tab') {
				uni.switchTab({
					url: path
				})
			} else {
				uni.navigateTo({
					url: path
				})
			}
        }
    }
}
</script>
<style lang="scss" scoped>
.comp-container {
    display: flex;
    flex-wrap: wrap;
    padding: 28upx 44upx;
    column-gap: 56upx;
    row-gap: 24upx;

    .module {
        width: calc(50% - 30upx);
        height: 200upx;
        line-height: 200upx;
        border-radius: 36upx;
        background-color: rgba(255,255,255,1);
        color: rgba(51,51,51,1);
        font-size: 32upx;
        text-align: center;
        border: 2upx solid rgba(187,187,187,1);
        box-sizing: border-box;
        image {
            width: 40upx;
            height: 40upx;
			margin-right: 10upx;
        }
    }
}
</style>