<template>
	<view class="newsWarp">
		<view class="news" v-for="(item,index) in news" :key="index">
			<view class="new" @tap="gotoInfo(item.post_id)">
				<view class="icon">
					<image class="image" :src="item.author_avatar" mode="aspectFit"></image>
				</view>
				<view class="content">
					<view class="title">
						{{item.title}}
					</view>
					<view class="text">
						{{item.summary}}
					</view>
					<view class="nameTime">
						<text>{{item.author_name}}</text>
						<text>{{item.updated_at}}</text>
					</view>
				</view>
			</view>
			
		</view>
	
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				news:[],
			}
		},
		onLoad() {
			uni.showLoading({
			    title: '加载中...'
			})
			uni.request({
			    url: 'https://unidemo.dcloud.net.cn/api/news', //仅为示例，并非真实接口地址。
			    method:'GET',
			    success: (res) => {
					uni.hideLoading()
			        // console.log(res.data);
			        this.news = res.data;
			    }
			});
			
		},
		methods: {
			gotoInfo(e){
				console.log(e)
				uni.navigateTo({
				    url: '../info/info?id='+e,
				    animationType: 'pop-in',
				    animationDuration: 200
				});
			}
		}
	}
</script>

<style scoped>
	.content {
		margin-left: 20upx;
	}
	.new{
		display: flex;
		padding: 20upx;
	}
	.icon{
		width: 200upx;
		height: 200upx;
	}
	.image{
		width: 200upx;
		height: 200upx;
	}
	.title{
		font-size: 36upx;
		font-weight: 700;
	}
	.text{
		font-size: 36upx;
	}
	.nameTime{
		display: flex;
		justify-content: space-between;
		font-size: 24upx;
		color: #999999;
	}
</style>
