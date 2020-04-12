<template>

	<view>
		<scroll-view scroll-x="true" class="scroll-content" :scroll-into-view="scrollTo">
			<view v-for="(item,index) in topBar" :key="index"
              :id="'top'+index"
			 class="scroll-item"
			 @tap="changeActive(index)"
			 >
				<text :class="index==activeIndex?'f-active-color':''">{{item.name}}</text>
			</view>
		</scroll-view>
		<!-- 实现导航栏原理，就是用轮播图和导航栏做关联，当导航栏滑动时轮播图也要滑动 -->
		<swiper :current="activeIndex" :style="'height:'+clientHeight+'px;'" @change="changeTab"> 
			<swiper-item v-for="(item,index) in topBar" :key="index">
				<!-- 推荐页面 -->
				<view class="home-data">
					<!-- <index-swiper></index-swiper>
					<recommend></recommend>
					<Card></Card>
					<commodity-list></commodity-list> -->
					<Banner></Banner>
					<Icon></Icon>
					<Card cardTitle='热销爆品'></Card>
					<Hot></Hot>
					<Card cardTitle='推荐店铺'></Card>
				    <Shop></Shop>
					<Card cardTitle='为您推荐'></Card>
					<CommodityList></CommodityList>
					 <div class="container">  
					        <mpvue-echarts :echarts="echarts" :onInit="onInit" />  
					    </div>  
				</view>
				<!-- 运动页面 -->
				
			</swiper-item>
			
		</swiper>
		
		
	</view>
</template>

<script>
	import indexSwiper from "../../components/index/indexSwiper.vue";
	import recommend from "../../components/index/recommend.vue";
	import Card from "../../components/common/Card.vue";
	import CommodityList from "../../components/common/CommodityList.vue";
	import Banner from "../../components/index/Banner.vue";
	import Icon from "../../components/index/Icons.vue";
	import Hot from "../../components/index/Hot.vue";
	import Shop from "../../components/index/Shop.vue";
	import * as echarts from 'echarts' ; 
	import mpvueEcharts from 'mpvue-echarts';
	export default {
		data() {
			return {
				//默认选中导航栏
				activeIndex:0,
				clientHeight:0,
				scrollTo:"top0",
				topBar: [{
						name: '推荐'
					},
					{
						name: '运动户外'
					},
					{
						name: '服饰内衣'
					},
					{
						name: '鞋靴箱包'
					},
					{
						name: '美妆个护'
					},
					{
						name: '家居数码'
					},
					{
						name: '食品母婴'
					}
				]
			}
		},
		methods: {
         changeActive(index){
			 if(index==this.activeIndex){
				 return ;
			 }
			 this.activeIndex=index;
			 this.scrollTo="top"+index;
			 
		 },
		 changeTab(e){
			this.changeActive(e.detail.current)
		 }
		},
		components: {
			indexSwiper,
			recommend,
			Card,
			CommodityList,
			Banner,
			Icon,
			Hot,
			Shop,
		    mpvueEcharts  
		},
		onLoad() {
			
		},
		onReady(){
		 let view = uni.createSelectorQuery().select(".home-data");
		view.boundingClientRect(data => {
		     this.clientHeight = data.height
		 }).exec();
		 uni.request({
		  url:"http://192.168.43.145:3000/index",
		   success:(res)=>{


		 				console.log(res.data)
		 			}
		 })
		 },
			 
		
		}
	
</script>

<style scoped>
	.scroll-content {
		width: 100%;
		height: 80rpx;
		white-space: nowrap;
	}

	.scroll-item {
		display: inline-block;
		padding: 10rpx 30rpx;
		font-size: 32rpx;
	}

	.f-active-color {
		padding: 10rpx 0;
		border-bottom: 6rpx solid #49BDFB;
	}
</style>
