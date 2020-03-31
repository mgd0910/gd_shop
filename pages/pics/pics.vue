<template>
	<view class="pics">
		<scroll-view class="left" scroll-y="true">
			<view 
				:class="active===i?'active':''"
				v-for="(v,i) in cates"
				:key="i"
				@click="leftClickHandle(i,v.id)"
			>
				{{v.title}}
			</view>
		</scroll-view>
		<scroll-view class="right" scroll-y="true">
			<view 
				class="item"
				v-for="(v,i) in secondDate"
				:key="i"
			>
				<image @click="previewImg(v.img_url)" :src="v.img_url"></image>
				<text>{{v.title}}</text>
			</view>
			<text v-if="secondDate.length === 0">暂无数据</text>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				cates:[],
				active:0,
				secondDate:[]
			}
		},
		onLoad() {
			this.getPicsCate()
		},
		methods: {
			async getPicsCate(){
				const res = await this.$myRequest({
					url:'/api/getimgcategory'
				})
				this.cates=res.data.message;
				this.leftClickHandle(0,this.cates[0].id)
			},
			async leftClickHandle(i,id){
				this.active=i;
				const res = await this.$myRequest({
					url:'/api/getimages/'+id
				})
				this.secondDate=res.data.message;
			},
			previewImg(current){
				const urls = this.secondDate.map(item=>{
					return item.img_url
				})
				uni.previewImage({
					urls,
					current
				})
			}
		}
	}
</script>

<style lang="scss">
	page{
		height:100%
	}
	.pics{
		height: 100%;
		display: flex;
		.left{
			width: 200rpx;
			height: 100%;
			border-right: 1px solid #eee;
			view{
				height: 60px;
				line-height: 60px;
				color: #333;
				text-align: center;
				font-size: 30rpx;
				border-top: 1px solid #eee;
			}
			.active{
				background-color: $shop-color;
				color: #fff;
			}
		}
		.right{
			height: 100%;
			width: 520rpx;
			margin:10rpx auto;
			.item{
				image{
					width: 520rpx;
					height: 520rpx;
					border-radius: 5px;
				}
				text{
					font-size: 30rpx;
					line-height: 60rpx;
				}
			}
		}
	}
</style>
