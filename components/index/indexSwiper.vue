<template>
	
	<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
		<swiper-item>
			<view class="swiper-item">
				<image src="../../static/image/swiper1.jpg" mode=""></image>
			</view>
		</swiper-item>
		<swiper-item>
			<view class="swiper-item">
				<image src="../../static/image/swiper2.jpg"></image>
			</view>
		</swiper-item>
		<swiper-item>
			<view class="swiper-item">
				<image src="../../static/image/swiper3.jpg"></image>
			</view>
		</swiper-item>
	</swiper>
</template>

<script>
</script>

<style scoped>
	swiper{
		width: 100%;
		height: 400rpx;
	}
	image{
		width: 100%;
	}
</style>
