<template>
	<view class="goods_list">
		<goodsList @goodsItemClick="goGoodsDetail" :data="goods"></goodsList>
		<view 
			class="isOver"
			v-if="flag"
		>
			------已加载全部数据------
		</view>
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list.vue'
	
	export default {
		data() {
			return {
				pageIndex:1,
				goods:[],
				flag:false
			}
		},
		components:{
			goodsList
		},
		onLoad() {
			this.getGoodsList();
		},
		onReachBottom() {
			console.log(this.goods.length);
			if(this.goods.length<this.pageIndex*10) return this.flag=true;
			this.pageIndex++;
			this.getGoodsList();
		},
		onPullDownRefresh() {
			this.pageIndex = 1;
			this.goods = [];
			this.flag = false;
			setTimeout(()=>{
				this.getGoodsList(()=>{
					uni.stopPullDownRefresh()
				});
			},1000)
		},
		methods: {
			//获取商品列表数据
			async getGoodsList(callBack){
				const res = await this.$myRequest({
					url:"/api/getgoods?pageindex="+this.pageIndex
				})
				this.goods =[...this.goods,...res.data.message]
				callBack && callBack();
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
	.goods_list{
		background-color: #eee;
		
	}
	.isOver{
			width: 100%;
			height: 50rpx;
			line-height: 50rpx;
			text-align: center;
			font-size: 28rpx;
	}
</style>
