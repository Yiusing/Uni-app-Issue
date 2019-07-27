<template>
	<view>
		<button type="button" @click="togglePopup('middle-list')">居中弹出（滚动列表）</button>
		<view class="content">
			<text>content</text>
		</view>
		<uni-popup :show="type === 'middle-list'" position="middle" mode="fixed" @hidePopup="togglePopup('')">
			<view class="">
				标题
			</view>
			<scroll-view :scroll-y="true" class="uni-center center-box">
				<view v-for="(item, index) in list" :key="index" class="uni-list-item">滚动列表数据 {{ item }}</view>
			</scroll-view>
			<view class="">
				底部
			</view>
		</uni-popup>
	</view>
</template>

<script>
	import uniPopup from '@/components/uni-popup/uni-popup.vue'

	export default {
		components: {
			uniPopup
		},
		data() {
			return {
				type: '',
				list: ['1', '2', '3', '4', '5', '6', '7', '8', '9', '10'],
				
			};
		},
		methods: {
			togglePopup(type) {
				this.type = type;
			}
		}
	};
</script>
<style>
	page {
		display: flex;
		flex-direction: column;
		box-sizing: border-box;
		background-color: #fff
	}

	view {
		font-size: 28upx;
		line-height: inherit
	}

	button {
		margin: 200upx 0;
	}



	.center-box {
		width: 500upx;
		height: 500upx;
	}

	.uni-list-item {
		text-align: left;
		line-height: 80upx;
		border-bottom: 1px #f5f5f5 solid;
	}

	.uni-list-item:last-child {
		border: none;
	}

	.content {
		justify-content: center;
		text-align: center;
		height: 500px;
		background: #dedede;
		flex-direction: column;
	}
</style>