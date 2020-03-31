<template>
	<view class="contact">
		<image class="img" src="../../static/photo/pic1.jpg"></image>
		<view class="info">
			<view @click="callPhone">联系电话：18409441016 (点击拨打)</view>
			<view>联系地址：北宋国西北都护府天山区灵鹫宫1号</view>
		</view>
		<map 
			class="map" 
			:longitude="longitude" 
			:latitude="latitude" 
			:markers="markers" 
			:scale="scale">
		</map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude:116.596552,
				latitude:39.910609,
				markers:[
					{
						longitude:116.596552,
						latitude:39.910609,
						iconPath:"../../static/photo/gps.png",
						width:20,
						heigth:20
					}
				],
				scale:18
			}
		},
		methods: {
			callPhone(){
				uni.makePhoneCall({
					phoneNumber:"18409441016"
				})
			}
		}
	}
</script>

<style lang="scss">
 .contact{
	 .img{
		 width: 750rpx;
		 height: 320rpx;
	 }
	 .info{
		 padding: 10rpx 20rpx;
		 font-size: 30rpx;
		 view{
			 line-height: 80rpx;
			 border-bottom: 1px solid #eee;
		 }
	 }
	 .map{
		 width: 750rpx;
		 height: 750rpx;
	 }
 }
</style>
