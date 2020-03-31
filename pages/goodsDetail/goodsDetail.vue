<template>
	<view class="goods_detail">
		<swiper 
			:indicator-dots="true" 
			:autoplay="false" 
			:interval="3000" 
			:duration="1000"
		>
			<swiper-item v-for="(v,i) in swipers" :key="i">
				<image :src="v.src"></image>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id:0,
				swipers:[]
			}
		},
		onLoad(options) {
			this.id=options.id
			this.getSwipers()
		},
		methods: {
			async getSwipers(){
				const res = await this.$myRequest({
					url:"/api/getthumimages/"+this.id
				})
				this.swipers=res.data.message;
			}
		}
	}
</script>

<style lang="scss">
	.goods_detail{
		swiper{
			height: 700rpx;
			image{
				width: 100%;
				height: 100%;
			}
		}
	}
</style>
