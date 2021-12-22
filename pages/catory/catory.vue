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
		<!-- 左边活动选项 -->
		<scroll-view scroll-y scroll-with-animation class="tab-view" :scroll-top="scrollTop" :style="{height:height+'px',top:top+'px'}">
			<view v-for="(item,index) in leftTabbar" :key="index" class="tab-bar-item"
			 :data-current="index" @tap.stop="swichNav(index,item.id)">
				<text :class="[currentTab==index ? 'active' : '']">{{item.name}}</text>
			</view>			
			<view style="width: 100%;height: 120rpx;"></view>
		</scroll-view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				leftTabbar:[
					{
						id:0,
						name:'品牌推荐'
					},
					{
						id:1,
						name:'食品饮料'
					},
					{
						id:2,
						name:'穿戴服饰'
					},
					{
						id:3,
						name:'面部护理'
					},
					{
						id:4,
						name:'彩妆香水'
					},
					{
						id:5,
						name:'个人护理'
					},
					{
						id:6,
						name:'箱包皮具'
					},
					{
						id:7,
						name:'珠宝饰品'
					},
					{
						id:8,
						name:'家居家纺'
					},
					{
						id:9,
						name:'强身保健'
					},
					{
						id:10,
						name:'生鲜果肉'
					}
				],
				top:0,//距离顶部
				height: 0, //scroll-view高度
				currentTab: 0, //预设当前项的值
				scrollTop: 0 ,//tab标题的滚动条位置
			};
		},
		onLoad() {
			setTimeout(() => { //获取高度
				uni.getSystemInfo({
					success: (res) => {
						let header = 92;
						let top = 0;
						//#ifdef H5
						top = 44;
						//#endif
						this.height = res.windowHeight - uni.upx2px(header);
						this.top = top + uni.upx2px(header);
					}
				});
			}, 50)
		},
		methods:{
			swichNav(index,id){ //左边栏选择
				this.currentTab=index
			}
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
		.tab-view {
			width: 200rpx;
			position: fixed;
			left: 0;
			z-index: 10;
			background: #FFFFFF;
			.tab-bar-item {
				width: 200rpx;
				height: 110rpx;
				box-sizing: border-box;
				display: flex;
				align-items: center;
				justify-content: center;
				font-size: 10pt;
				color: #444;
				font-weight: 400;
				.active {
					color: #FFFFFF;
					background: #FF7104;
					padding: 8rpx 26rpx;
					border-radius: 50rpx;
				}
				
			}
		}
	}
</style>
