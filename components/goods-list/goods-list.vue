<template>
	<view class="goods_list">
		<view 
			class="goods_item" 
			v-for="(v,i) in data" 
			:key="i"
			@click="navigator(v.id)"
		>
			<image :src="v.img_url"></image>
			<view class="price">
				<text class="">¥{{v.sell_price}}</text>
				<text class="">¥{{v.market_price}}</text>
			</view>
			<view class="name">
				{{v.title}}
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		props:{
			data:{
				type:Array,
				required:true   //必填
			}
		},
		methods:{
			navigator(id){
				this.$emit("goodsItemClick",id)
			}
		}
	}
</script>

<style lang="scss">
	.goods_list {
		padding: 0 15rpx;
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;

		.goods_item {
			width: 355rpx;
			background-color: #fff;
			margin: 10rpx 0;
			padding: 15rpx;
			box-sizing: border-box;

			image {
				width: 80%;
				height: 300rpx;
				display: block;
				margin: 0 auto;
			}

			.price {
				color: $shop-color;
				font-size: 36rpx;
				margin: 20rpx 0 5rpx 0;

				text:nth-child(2) {
					color: #ccc;
					font-size: 28rpx;
					margin-left: 17rpx;
					text-decoration: line-through;
				}
			}

			.name {
				font-size: 28rpx;
				line-height: 50rpx;
			}
		}
	}
</style>
