<template>
	<view class="home_container">
		<view class="home_header">
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
					<search message="大家都在搜索" textAlign="56" frameColor="#FFFFFF" innerFrameColor="#F2F2F2"
						textColor="#555555" :borderRadius="56"></search>
				</view>
			</view>
		</view>
		<view class="home_bannersBox">
			<banners :bannerData="bannersData"></banners>
		</view>
		<view class="home_navBar">
			<navIcon class="navIcon_style" :list="navs" textColor="#353535" :rowNums="4" background="#ffffff"
				:listNums="3"></navIcon>
		</view>
		<view class="home_good_list">
			<vouchers :list='goods_ist'></vouchers>
		</view>
		<view class="home_ap-link">
			<text>广州景瑞科技有限公司版权所有</text>
			<text>粤ICP备19145623号</text>
		</view>
		<citySelect @back_city="back_city" v-if="cityselec"></citySelect>
	</view>
</template>

<script>
	import search from '@/components/search/search.vue';
	import banners from '@/components/banners/banners';
	import navIcon from '@/components/navIcon/navIcon';
	import vouchers from '@/components/vouchers/vouchers.vue';
	import citySelect from '@/components/linzq-home/linzq-city.vue';
	export default {
		components: {
			search,
			banners,
			navIcon,
			vouchers,
			citySelect
		},
		data() {
			return {
				bannersData: { //轮播图
					fill: 1,
					height: 390,
					style: 1,
					banners: [{
							openType: "navigate",
							params: [],
							picUrl: "https://www.mingyuanriji.cn/web//uploads/images/original/20211116/588858be835b03a9195657c7f004b5fe.jpg",
							url: "/oil/oilHome/oilHome"
						},
						{
							openType: "navigate",
							params: [],
							picUrl: "https://www.mingyuanriji.cn/web//uploads/images/original/20211014/bd6f29fb30b9388644e93af273c1917b.jpg",
							url: "/pages/diy/diy?page_id=133"
						}
					]
				},
				navs: [ //金刚区
					{
						icon: "https://www.mingyuanriji.cn/web//uploads/images/original/20211028/12582f156f4f10c272538c2c75698480.jpg",
						name: "热卖爆品",
						openType: "navigate",
						url: "/aggregation/sellingHot/sellingHot",
					},
				],
				goods_ist: [{ //商品
					cover_pic: "http://yingmlife-1302693724.cos.ap-guangzhou.myqcloud.com/uploads/images/original/20211018/af8287e1940ea564d15c60345c790bea.jpg",
					enable_express: "0",
					freight_id: "5",
					goods_stock: "79751",
					got_shopping_voucher_num: 0.1,
					id: "3483",
					is_level: "1",
					is_show_sales: "1",
					max_deduct_integral: "0.00",
					mch_id: "0",
					name: "牙刷成人软毛10-20支套装",
					original_price: "39.00",
					price: "0.10",
					sales: "已售1315件",
					status: "1",
					unit: "件",
					use_attr: "1",
					use_virtual_sales: "1",
					video_url: "",
					virtual_sales: "1256",
				}],
				cityselec:false,//城市选择
			}
		},
		methods:{
			setCITY(){ //选择城市
				this.cityselec = true
			},
			back_city(e) { //城市选择回显
				if (e !== 'no') {
					this.cityselec = false;
				} else {
					this.cityselec = false;
				}
			},
		}
	}
</script>

<style lang="less">
	.home_container {
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

			.checksao {
				width: 35%;
				background: #fff;
				position: relative;

				.citiLOGO_location {
					width: 50rpx;
					height: 96rpx;
					position: absolute;
					top: 0;
					left: 20rpx;
					z-index: 9999;

					image {
						width: 40rpx;
						height: 40rpx;
						display: block;
						margin-top: 33rpx;
					}
				}

				.citiLOGO_select {
					width: 30rpx;
					height: 96rpx;
					position: absolute;
					top: 10rpx;
					right: 0rpx;
					z-index: 9999;

					image {
						width: 20rpx;
						height: 20rpx;
						display: block;
						margin-top: 33rpx;
					}
				}
			}

			.search {
				width: 75%;
				margin-bottom: 30rpx;
			}
		}

		.home_bannersBox {
			margin-top: 90rpx;
		}
		.home_ap-link{
			width: 100%;
			height: 30rpx;
			margin-bottom: 120rpx;
			text-align: center;
			font-size: 25rpx;
			text{
				display: block;
				width: 100%;
				overflow: hidden;
				margin-top: 10rpx;
			}
		}
	}
</style>
