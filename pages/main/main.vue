<template>
	<view class="main-wrap">
		<uni-search-bar placeholder="请输入搜索内容" cancelButton="none" @confirm="search"></uni-search-bar>
		<view class="uni-padding-wrap">
			<swiper class="swiper" autoplay="true" circular="true" interval="1000" duration="500" indicator-dots="true">
				<swiper-item v-for="(item,index) in swiperArr" :key="index">
					<image :src="item.src" @tap="previewImage(index)" class="swiper-item-image"></image>
				</swiper-item>
			</swiper>
		</view>
		<view class="uni-padding-wrap">
			<news-list-item v-for="(item,index) in newsLists" :itemData="item"></news-list-item>
		</view>
	</view>
</template>

<script>
	// 引入组件
	import {
		uniSearchBar,
		uniSwiperDot
	} from '@dcloudio/uni-ui'
	// 引入自定义组件
	import newsListItem from '@/components/newsListItem.vue'
	
	// 引入图片
	import banner from "@/static/img/banner/banner.png"
	import img01 from "@/static/img/newsImg/img01.png"
	import img03 from "@/static/img/newsImg/img03.jpeg"

	export default {
		data() {
			return {
				swiperArr: [{
					content: '内容 A',
					src:banner
				}, 
				{
					content: '内容 B',
					src:banner
				}, 
				{
					content: '内容 C',
					src:banner
				},
				{
					content: '内容 D',
					src:banner
				},
				{
					content: '内容 E',
					src:banner
				}],
				newsLists:[
					{
					title:"华为手机对比苹果，对比的结果真的惊了对比的结果真的惊了对比的结果真的惊了！",
					id:"1",
					companyName:"who聊科技",
					commentsNumber:4,
					time:"1590559666729",
					imgLists:[]
				},
				{
					title:"不用数据流量也能上网，这个操作太秀了！",
					id:"1",
					companyName:"who聊科技",
					commentsNumber:4,
					time:"1576585605000",
					imgLists:[
						{
							imgId:"1",
							src:img01
						},
						{
							imgId:"2",
							src:img01
						}
					]
				},
				{
					title:"现在这些假新闻都起的什么垃圾题目，真的是辣眼睛辣眼睛辣眼睛辣眼睛辣眼睛辣眼睛辣眼睛",
					id:"1",
					companyName:"who聊科技",
					commentsNumber:200,
					time:"1576585605369",
					imgLists:[
						{
							imgId:"1",
							src:img03
						},
						{
							imgId:"4",
							src:img03
						},
						{
							imgId:"90",
							src:img03
						}
					]
				},
				{
					title:"不用数据流量也能上网，这个操作太秀了！",
					id:"1",
					companyName:"who聊科技",
					commentsNumber:4,
					time:"1576585605000",
					imgLists:[
						{
							imgId:"1",
							src:img01
						},
						{
							imgId:"2",
							src:img01
						}
					]
				},
				]
			}
		},
		components: {
			uniSearchBar,
			uniSwiperDot,
			newsListItem
		},
		computed:{
			
		},
		onLoad() {
		},
		methods:{
			// 搜索
			search(value){
				console.log("搜索框的输入值：",value)
			},
			previewImage(index) {
				let arr = this.swiperArr.map(item=>{
					return item.src
				})
				uni.previewImage({
					current:index, //预览图片的下标
					urls:arr //预览图片的地址，必须要数组形式，如果不是数组形式就转换成数组形式就可以
				})
			}
		}
	}
</script>

<style>
	.main-wrap {
		overflow-y: scroll;
	}
	.swiper-item-image {
		width: 100%;
		height: 100%;
	}
</style>
