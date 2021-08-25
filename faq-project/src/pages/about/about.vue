<template>
	<view class="contact">
		<image class="img" src="http://www.itcast.cn/2018czydz/images/gywmban.jpg"></image>
		<view class="info">
			<view @click="phone">联系电话：0351-3922280（点击拨打）</view>
			<view>联系地址：山西省太原市中北大学</view>
			<button @click="goGame">井字棋小游戏</button>
		</view>
		<map class="map" :longitude="longitude" :latitude="latitude"
		      :markers="markers" :scale="scale"></map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude:112.453582,
				latitude: 38.02132,
				scale:13,
				markers:[
					{
						longitude:112.453582,
						latitude: 38.02132,
						iconPath:'../../static/icon/zbdx.png',
						width:30,
						height:30
					}
				] 
			}
		},
		methods: {
			phone(){
				uni.makePhoneCall({
					phoneNumber:'0351-3922280'
				})
			},
			goGame(){
				uni.navigateTo({
					url:'game/game'
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
