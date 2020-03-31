<template>
	<view class="index">
		<!-- 轮播区 start -->
		<swiper :indicator-dots="true" :autoplay="true" :circular="true" :interval="3000" :duration="1000">
			<swiper-item v-for="(v,i) in swiperList" :key="i">
				<image :src="v.img" mode=""></image>
			</swiper-item>
		</swiper>
		<!-- 轮播区 end -->
		<!-- 导航区 start -->
		<view class="nav">
			<view 
				class="nav_item"
				v-for="(v,i) in navs"
				:key="i"
				@click="navItemClick(v.path)"
			>
				<view :class="v.icon"></view>
				<text>{{v.title}}</text>
			</view>
		</view>
		<!-- 导航区 start -->
		<!-- 推荐商品区 start -->
		<view class="hot_goods">
			<view class="tit">推荐商品</view>
			<goodsList @goodsItemClick="goGoodsDetail" :data="goods"></goodsList>
		</view>
		<!-- 推荐商品区 end -->
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list.vue'
	export default {
		data() {
			return {
				swiperList:[],
				goods:[],
				navs:[
					{
						icon:"iconfont icon-ziyuan",
						title:"果冻超市",
						path:'/pages/goods/goods'
					},
					{
						icon:"iconfont icon-guanyuwomen",
						title:"联系我们",
						path:'/pages/contact/contact'
					},
					{
						icon:"iconfont icon-tupian",
						title:"社区图片",
						path:'/pages/pics/pics'
					},
					{
						icon:"iconfont icon-shipin",
						title:"学习视频",
						path:'/pages/videos/videos'
					}
				]
			}
		},
		components:{
			goodsList
		},
		onLoad() {
			this.getSwiper();
			this.getHotGoods();
		},
		
		methods: {
			//获取轮播图数据
			async getSwiper(){
				const res = await this.$myRequest({
					url:'/api/getlunbo'
				})
				console.log(res);
				this.swiperList=res.data.message
			},
			//获取热门商品列表数据
			async getHotGoods(){
				const res = await this.$myRequest({
					url:"/api/getgoods?pageindex=1"
				})
				console.log(res)
				this.goods=res.data.message;
			},
			// 导航点击处理函数
			navItemClick(url){
				uni.navigateTo({
					url
				})
			},
			// 导航到商品详情页
			goGoodsDetail(id){
				uni.navigateTo({
					url:"../goodsDetail/goodsDetail?id="+id
				})
			}
		}
	}
</script>

<style lang="scss">
	.index{
		swiper{
			width: 750rpx;
			height: 380rpx;
			image{
				width: 100%;
				height: 100%;
			}
		}
		.nav{
			display: flex;
			.nav_item{
				width: 25%;
				text-align: center;
				view{
					width: 120rpx;
					height: 120rpx;
					background-color: $shop-color;
					border-radius: 50%;
					margin:10rpx auto;
					line-height: 120rpx;
					color: #fff;
					font-size: 50rpx;
				}
				text{
					font-size: 30rpx;
				}
				.icon-tupian{
					font-size: 45rpx;
				}
			}
		}
		.hot_goods{
			background-color: #eee;	
			overflow: hidden;
			margin-top: 20rpx;
			.tit{
				height: 100rpx;
				line-height: 100rpx;
				color: $shop-color;
				text-align: center;
				letter-spacing: 40rpx;
				background-color: #fff;
				margin:7rpx 0;
			}
		}
	}
</style>
