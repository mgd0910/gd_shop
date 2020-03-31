<template>
	<view class="news">
		<newsItem @itemClick="goDetail" :data="newsList"></newsItem>
	</view>
</template>

<script>
	import newsItem from '../../components/news-item/news-item.vue'
	export default {
		data() {
			return {
				newsList:[]
			}
		},
		onLoad() {
			this.getNews();
		},
		components:{
			newsItem
		},
		methods: {
			async getNews(){
				const res = await this.$myRequest({
					url:"/api/getnewslist"
				})
				this.newsList=res.data.message;
			},
			goDetail(id){
				uni.navigateTo({
					url:"../newsDetail/newsDetail?id="+id
				})
			}
		}
	}
</script>

<style lang="scss">
	
</style>
