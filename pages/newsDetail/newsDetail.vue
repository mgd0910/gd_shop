<template>
	<view class="news_detail">
		<text class="title">{{detail.title}}</text>
		<view class="info">
			<text>发表时间：{{detail.add_time | formatData}}</text>
			<text>浏览次数：{{detail.click}}</text>
		</view>
		<!-- <view class="content" v-html="detail.content"></view> -->
		<view class="content">
			<rich-text :nodes="detail.content"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id:0,
				detail:{}
			}
		},
		onLoad(options) {
			this.id=options.id;
			this.getNewsDetail();
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
		methods: {
			async getNewsDetail(){
				const res = await this.$myRequest({
					url:'/api/getnew/'+this.id
				})
				this.detail=res.data.message[0];
			}
		}
	}
</script>

<style lang="scss">
	.news_detail{
		font-size: 30rpx;
		padding: 0 20rpx;
		.title{
			width: 710rpx;
			text-align: center;
			display: block;
			margin:20rpx 0;
		}
		.info{
			display: flex;
			justify-content: space-between;
		}
	}
</style>
