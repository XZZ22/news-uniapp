<template>
	<view>
		<view class="news-item-type-wrap" v-if="itemData.imgLists.length===0">
			<view class="news-item-type-title">{{itemData.title}}</view>
			<view class="news-item-type-message">
				<text class="news-item-type-message-text">{{itemData.companyName}}</text>
				<text class="news-item-type-message-text">评论 {{itemData.commentsNumber}}</text>
				<text class="news-item-type-message-text">{{itemData.time | formatTime}}</text>
			</view>
		</view>
		<view class="news-item-type-wrap2" v-if="itemData.imgLists.length>0 && itemData.imgLists.length<3 ">
			<view class="news-item-type-wrap-left">
				<view class="news-item-type-wrap-left-title">
					{{itemData.title}}
				</view>
				<view class="news-item-type-wrap-left-message">
					<text class="news-item-type-wrap-left-message-text">{{itemData.companyName}}</text>
					<text class="news-item-type-wrap-left-message-text">评论 {{itemData.commentsNumber}}</text>
					<text class="news-item-type-wrap-left-message-text">{{itemData.time | formatTime}}</text>
				</view>
			</view>
			<view class="news-item-type-wrap-right">
				<image class="news-item-type-wrap-right-image" @tap="previewImage(index)" :src="item.src" mode="aspectFit" v-for="(item,index) in itemData.imgLists" :key="item.imgId"></image>
			</view>
		</view>
		<view class="news-item-type-wrap3" v-if="itemData.imgLists.length>2">
			<view class="news-item-type-wrap3-title">
				{{itemData.title}}
			</view>
			<view class="news-item-type-wrap3-image">
				<image class="news-item-type-wrap3-image-item" @tap="previewImage(index)" :src="item.src" mode="aspectFit" v-for="(item,index) in itemData.imgLists" :key="item.imgId"></image>
			</view>
			<view class="news-item-type-wrap3-message">
				<text class="news-item-type-message-text">{{itemData.companyName}}</text>
				<text class="news-item-type-message-text">评论 {{itemData.commentsNumber}}</text>
				<text class="news-item-type-message-text">{{itemData.time | formatTime}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	import mIcon from './m-icon/m-icon.vue'
	import {formatMsgTime} from "@/utils/formatMsgTime.js"
	export default {
		components: {
			mIcon
		},
		props: {
			itemData:{
				type:Object,
				default() {
					return {
						title:"",
						id:"",
						companyName:"",
						commentsNumber:0,
						time:"",
						imgLists:[]
					}
				}
			}
		},
		data() {
			return {
			}
		},
		filters:{
			formatTime(value){
				return formatMsgTime(value)
			}
		},
		computed: {
		},
		methods: {
			previewImage(index) {
				let arr = this.itemData.imgLists.map(item=>{
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

<style lang="scss" scoped>
	.news-item-type-wrap {
		padding:8px 0px;
		.news-item-type-title {
			font-size: 18px;
		}
		.news-item-type-message {
			font-size: 12px;
			color: #CCCCCC;
			.news-item-type-message-text {
				margin:0 5px ;
			}
		}
	}
	.news-item-type-wrap2 {
		max-height:130px;
		border-top:1px solid #ccc;
		padding:8px 0px;
		display:flex;
		.news-item-type-wrap-left {
			width:60%;
			heigth:100%;
			display:flex;
			flex-direction:column;
			justify-content:space-around;
			.news-item-type-wrap-left-title {
				font-size: 18px;
			}
			.news-item-type-wrap-left-message {
				font-size: 12px;
				color: #CCCCCC;
				.news-item-type-wrap-left-message-text {
					margin:0 5px ;
				}
			}
		}
		.news-item-type-wrap-right {
			width:40%;
			heigth:100%;
			display:flex;
			.news-item-type-wrap-right-image {
				width:100%;
				max-height:100px;
				margin-right:2px;
			}
		}
	}
	.news-item-type-wrap3 {
		border-top:1px solid #ccc;
		padding:8px 0px;
		.news-item-type-wrap3-title {
			font-size:18px;
		}
		.news-item-type-wrap3-image {
			display:flex;
			.news-item-type-wrap3-image-item {
				width:100%;
				max-height:120px;
				margin-right:2px;
			}
		}
		.news-item-type-wrap3-message {
			font-size: 12px;
			color: #CCCCCC;
			.news-item-type-message-text {
				margin:0 5px ;
			}
		}
	}
	
	
</style>
