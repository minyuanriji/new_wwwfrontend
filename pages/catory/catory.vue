<template>
	<view class="catory_container">
		<view class="catory-searchbox">
			<view class="catory-search-input" @tap="search">
				<!-- #ifdef APP-PLUS || MP -->
				<icon type="search" size='13' color='#999'></icon>
				<!-- #endif -->
				<text class="catory-search-text">搜索商品</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		}
	}
</script>

<style lang="less">
	.catory_container{
		width: 100%;
		overflow: hidden;
		.catory-searchbox {
			width: 100%;
			height: 92rpx;
			padding: 0 30rpx;
			box-sizing: border-box;
			background: #fff;
			display: flex;
			align-items: center;
			justify-content: center;
			position: fixed;
			left: 0;
			top: 0;
			/* #ifdef H5 */
			top: 44px;
			/* #endif */
			z-index: 100;
			.catory-search-input {
				width: 100%;
				height: 60rpx;
				background: #f1f1f1;
				border-radius: 30rpx;
				font-size: 11pt;
				color: #999;
				display: flex;
				align-items: center;
				justify-content: center;
				.catory-search-text {
					padding-left: 16rpx;
				}
			}
		}
		
		.catory-searchbox::after {
			content: '';
			position: absolute;
			border-bottom: 1rpx solid #d2d2d2;
			-webkit-transform: scaleY(0.5);
			transform: scaleY(0.5);
			bottom: 0;
			right: 0;
			left: 0;
		}
	}
</style>
