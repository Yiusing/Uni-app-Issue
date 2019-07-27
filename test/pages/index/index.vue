<template>
	<view class="content">
		<button type="primary" @click="toPopup">Popup</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello'
			}
		},
		onLoad() {

		},
		methods: {
			toPopup() {
				uni.navigateTo({
					url:"../popup/popup"
				})
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding-top:10rpx;
	}

</style>
