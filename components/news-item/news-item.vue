<template>
	<view>
		<view
			class="news_item"
			v-for="(v,i) in data"
			:key="i"
			@click="navigator(v.id)"
		>
			<image :src="v.img_url"></image>
			<view class="right">
				<view class="tit">
					{{v.title}}
				</view>
				<view class="info">
					<text>发表时间：{{v.add_time | formatData}}</text>
					<text>浏览次数：{{v.click}}</text>
				</view>
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
		filters:{
			formatData(data){
				const nDate=new Date(data);
				const year = nDate.getFullYear().toString().padStart(2,0);
				const month = nDate.getMonth().toString().padStart(2,0);
				const day = nDate.getDay().toString().padStart(2,0);
				return year +'-'+ month +'-'+ day
			}
		},
		methods:{
			navigator(id){
				this.$emit("itemClick",id)
			}
		}
	}
</script>

<style lang="scss">
	.news_item{
		display: flex;
		padding: 10rpx 20rpx;
		border-bottom:1px solid $shop-color;
		image{
			width: 200rpx;
			min-width: 200rpx;
			height:150rpx ;
			min-height: 150rpx;
		}
		.right{
			margin-left: 15rpx;
			display: flex;
			flex-direction: column;
			justify-content: space-between;
			.tit{
				font-size: 30rpx;
			}
			.info{
				font-size: 24rpx;
				text:nth-child(2){
					margin-left: 30rpx;
				}
			}
		}
		
	}
</style>
