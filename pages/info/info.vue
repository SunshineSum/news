<template>
	<view class="newsWarp">
		<view class="new" >
			<view class="content">
				<view class="title">
					{{title}}
				</view>
				<view class="text">
					{{summary}}
				</view>
				<view class="text">
					<rich-text :nodes="content"></rich-text>
				</view>
				<view class="nameTime">
					<text>{{author_name}}</text>
					<text>{{updated_at}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title:'',
				summary:'',
				author_name:'',
				updated_at:'',
				content:''
			}
		},
		onLoad(e) {
			// console.log(e,'id')
			uni.showLoading({
			    title: '加载中...'
			})
			uni.request({
			    url: 'https://unidemo.dcloud.net.cn/api/news/36kr/'+e.id, //仅为示例，并非真实接口地址。
			    method:'GET',
			    success: (res) => {
					uni.hideLoading()
			        // console.log(res.data);
					this.title=res.data.title
					this.summary=res.data.summary
					this.author_name=res.data.author_name
					this.updated_at=res.data.updated_at
					this.content=res.data.content
			    }
			});
			
		},
		methods: {
			
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
	.title{
		font-size: 48upx;
		font-weight: 700;
	}
	.text{
		font-size: 36upx;
		font-weight: 700;
	}
	.nameTime{
		display: flex;
		justify-content: space-between;
		font-size: 24upx;
		color: #999999;
	}
</style>
