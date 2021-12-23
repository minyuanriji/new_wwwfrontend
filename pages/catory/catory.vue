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
		<block v-for="(item,index) in leftTabbar" :key="index">
			<scroll-view scroll-y class="right-box" :style="{height:height+'px',top:top+'px'}" v-if="currentTab==index">
				<view class="page-view">
					<!-- 轮播图 -->
					<swiper indicator-dots autoplay circular :interval="5000" :duration="150" class="swiper">
						<block v-for="(items,indexs) in leftTabbar" :key='indexs'>
							<swiper-item v-if="items.advert_pic != ''" @tap.stop="detail(items.advert_url)">
								<image :src="items.advert_pic" class="slide-image" />
							</swiper-item>
						</block>
					</swiper>					
					<!-- 右边商品楼层 -->
					<view class="class-box">
						<view class="class-item" v-for="(citem,index) in leftTabbar[currentTab].child" :key="index">
							<view class="class-name">{{citem.name}}</view>
							<view class="g-container">
								<view class="g-box" v-for="(pitem,i) in citem.child" :key="i" @tap.stop="productList($event,pitem.id,leftTabbar[currentTab].id)" :data-key="pitem.name">
									<image :src="pitem.pic_url" class="g-image" />
									<view class="g-title">{{pitem.name}}</view>
								</view>
							</view>
						</view>
						<view style="width: 100%;height: 120rpx;"></view>
					</view>
				</view>
			</scroll-view>
		</block>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				leftTabbar:[
					{
						id:0,
						name:'品牌推荐',
						advert_pic:'http://yingmlife-1302693724.cos.ap-guangzhou.myqcloud.com/uploads/images/original/20200928/5e0c9bc7b73d4bb56d2c18a97c74558e.png',
						child:[
							{
								name:'品牌',
								child:[
									{
										pic_url:'http://yingmlife-1302693724.cos.ap-guangzhou.myqcloud.com/uploads/images/original/20200903/64f7858157eaaf2aff0b8be567fdd67a.png',
										name:'迪奥'
									},
									{
										pic_url:'http://yingmlife-1302693724.cos.ap-guangzhou.myqcloud.com/uploads/images/original/20200903/b7f502b073d0f63e04483dc2d809e2cc.jpg',
										name:'SK-II'
									}
								]							
							}
						]
					},
					{
						id:1,
						name:'食品饮料',
						advert_pic:'http://yingmlife-1302693724.cos.ap-guangzhou.myqcloud.com/uploads/images/original/20200928/5e0c9bc7b73d4bb56d2c18a97c74558e.png'
					},
					{
						id:2,
						name:'穿戴服饰',
						advert_pic:'http://yingmlife-1302693724.cos.ap-guangzhou.myqcloud.com/uploads/images/original/20200928/5e0c9bc7b73d4bb56d2c18a97c74558e.png'
					},
					{
						id:3,
						name:'面部护理',
						advert_pic:'http://yingmlife-1302693724.cos.ap-guangzhou.myqcloud.com/uploads/images/original/20200928/5e0c9bc7b73d4bb56d2c18a97c74558e.png'
					},
					{
						id:4,
						name:'彩妆香水',
						advert_pic:'http://yingmlife-1302693724.cos.ap-guangzhou.myqcloud.com/uploads/images/original/20200928/5e0c9bc7b73d4bb56d2c18a97c74558e.png'
					},
					{
						id:5,
						name:'个人护理',
						advert_pic:''
					},
					{
						id:6,
						name:'箱包皮具',
						advert_pic:''
					},
					{
						id:7,
						name:'珠宝饰品',
						advert_pic:''
					},
					{
						id:8,
						name:'家居家纺',
						advert_pic:''
					},
					{
						id:9,
						name:'强身保健',
						advert_pic:''
					},
					{
						id:10,
						name:'生鲜果肉',
						advert_pic:''
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
		.right-box {
			width: 100%;
			position: fixed;
			padding-left: 220rpx;
			box-sizing: border-box;
			left: 0;
			.page-view {
				width: 100%;
				overflow: hidden;
				padding-top: 20rpx;
				padding-right: 20rpx;
				box-sizing: border-box;
				padding-bottom: env(safe-area-inset-bottom);
				.swiper {
					width: 100%;
					height: 220rpx;
					border-radius: 12rpx;
					overflow: hidden;
					transform: translateZ(0);
					.slide-image {
						width: 100%;
						height: 220rpx;
					}
					/* #ifdef APP-PLUS || MP */
					.wx-swiper-dot {
						width: 8rpx;
						height: 8rpx;
						display: inline-flex;
						background: none;
						justify-content: space-between;
					}					
					.wx-swiper-dot::before {
						content: '';
						flex-grow: 1;
						background: rgba(255, 255, 255, 0.8);
						border-radius: 16rpx;
						overflow: hidden;
					}					
					.wx-swiper-dot-active::before {
						background: #fff;
					}					
					.wx-swiper-dot.wx-swiper-dot-active {
						width: 16rpx;
					}		
					/* #endif */
					/* #ifdef H5 */
					.uni-swiper-dot {
						width: 8rpx;
						height: 8rpx;
						display: inline-flex;
						background: none;
						justify-content: space-between;
					}					
					.uni-swiper-dot::before {
						content: '';
						flex-grow: 1;
						background: rgba(255, 255, 255, 0.8);
						border-radius: 16rpx;
						overflow: hidden;
					}					
					.uni-swiper-dot-active::before {
						background: #fff;
					}					
					.uni-swiper-dot.uni-swiper-dot-active {
						width: 16rpx;
					}				
					/* #endif */	
				}
				.class-box {
					padding-top: 30rpx;
					.class-item {
						background: #fff;
						width: 100%;
						box-sizing: border-box;
						padding: 20rpx;
						margin-bottom: 20rpx;
						border-radius: 12rpx;
						.class-name {
							font-size: 9pt;
						}
						.g-container {
							display: flex;
							display: -webkit-flex;
							justify-content: flex-start;
							flex-direction: row;
							flex-wrap: wrap;
							.g-box {
								width: 33.3333%;
								text-align: center;
								padding-top: 40rpx;
								.g-image {
									width: 120rpx;
									height: 120rpx;
								}
								.g-title {
									font-size: 9pt;
								}
							}
						}												
					}
				}	
			}
		}
	}
</style>
