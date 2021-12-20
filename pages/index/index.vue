<template>
	<view class="home_container">
		<view class="header">
			<view class="search_box">
				<view class="checksao">
					<view style="width: 80%;color: #000;font-size: 30rpx;font-weight: bold;overflow: hidden;
					text-overflow:ellipsis;white-space: nowrap;margin-left: 30rpx;" @click="setCITY">
						<view style="padding-top: 30rpx;padding-left: 35rpx;box-sizing: border-box;overflow: hidden;
					text-overflow:ellipsis;white-space: nowrap;">加载中...</view>
					</view>
					<view class="citiLOGO_location">
						<image src="https://dev.mingyuanriji.cn/web/plugins//hone_logo.png" mode=""></image>
					</view>
					<view class="citiLOGO_select">
						<image src="https://dev.mingyuanriji.cn/web/plugins//home_up.png" mode=""></image>
					</view>
				</view>	
				<view class="search">
					<search message="大家都在搜索" textAlign="56" frameColor="#FFFFFF"
					 innerFrameColor="#F2F2F2" textColor="#555555" :borderRadius="56"></search>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import search from '@/components/search/search.vue';
	export default{
		components:{
			search
		},
		data(){
			return{
				
			}
		}
	}
</script>

<style lang="less">
	.home_container{
		width: 100%;
		overflow: hidden;
		.search_box {
			position: fixed;
			/* #ifdef H5||MP*/
				top: 80rpx;
				height: 100rpx;
			/* #endif */
			width: 100%;
			/* #ifdef APP-PLUS */
				top: 40rpx;
				height: 100rpx;
			/* #endif */
			z-index: 99;
			display: flex;
			background: #fff;
			.checksao{
				width: 35%;
				background: #fff;
				position: relative;
				.citiLOGO_location{
					width: 50rpx;
					height: 96rpx;
					position: absolute;
					top: 0;
					left: 20rpx;
					z-index:9999;
					image{
						width: 40rpx;
						height: 40rpx;
						display: block;
						margin-top: 33rpx;
					}
				}
				.citiLOGO_select{
					width: 30rpx;
					height: 96rpx;
					position: absolute;
					top: 10rpx;
					right:0rpx;
					z-index:9999;
					image{
						width: 20rpx;
						height: 20rpx;
						display: block;
						margin-top: 33rpx;
					}
				}
			}
			.search{
				width: 75%;
				margin-bottom: 30rpx;
			}
		}
		
	}
</style>
