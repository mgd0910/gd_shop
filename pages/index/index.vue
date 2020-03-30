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
			<view class="nav_item">
				<view class="iconfont icon-ziyuan"></view>
				<text>果冻超市</text>
			</view>
			<view class="nav_item">
				<view class="iconfont icon-guanyuwomen"></view>
				<text>联系我们</text>
			</view><view class="nav_item">
				<view class="iconfont icon-tupian"></view>
				<text>社区图片</text>
			</view><view class="nav_item">
				<view class="iconfont icon-shipin"></view>
				<text>学习视频</text>
			</view>
		</view>
		<!-- 导航区 start -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				swiperList:[]
			}
		},
		onLoad() {
			this.getSwiper();
		},
		
		methods: {
			//获取轮播图数据
			async getSwiper(){
				const res = await this.$myRequest({
					url:'/api/getlunbo'
				})
				console.log(res);
				this.swiperList=res.data.message
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
					background-color: #b50e03;
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
	}
</style>
