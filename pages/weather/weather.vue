<template>
	<view>
		<view class="head">
			<view class="weather">
				{{province}}
			</view>
			<view class="weather">
				更新时间:{{reporttime}}
			</view>
		</view>
		<!-- <view class="content" :style="{background: 'url('+imageURL+')'}"> -->
		<view class="content">
			<view class="text">
				城市：{{city}}
			</view>
			<view class="text">
				天气：{{weather}}
			</view>
			<view class="text">
				温度：{{temperature}}
			</view>
			<view class="text">
				风向：{{winddirection}}
			</view>
			<view class="text">
				风力：{{windpower}}
			</view>
			<view class="text">
				湿度：{{humidity}}
			</view>
			
		</view>
	</view>
</template>

<script>
	import amapFile from '../../common/adress/amap-wx.js'
	export default{
		data(){
			return{
				key:'7497c68043d31ea429ca233b876a10f5',
				myAmapFun:null,
				imageURL:'/../../static/weather1.jpg',
				province: '',
				city: '',
				adcode: '',
				weather: '',
				temperature: '',
				winddirection: '',
				windpower: '',
				humidity: '',
				reporttime: ''			
			}
		},
		onLoad() {
			// #ifdef APP-PLUS
			this.myAmapFun = new amapFile.AMapWX({key:this.key});
			// #endif
		    
		},
		onShow() {
			// #ifdef APP-PLUS
			this.weatherFn()
			// #endif
			
		},
		methods:{
			weatherFn(){
				uni.showLoading({
				    title: '加载中...'
				})
				// console.log('111111111')
				var that = this;
				that.myAmapFun.getWeather({
				  success: function(data){
					//成功回调
					uni.hideLoading()
					// console.log(JSON.stringify(data),'weather')
					that.city=JSON.stringify(data.city.data).replace(/\"/g, "")
					that.weather=JSON.stringify(data.weather.data).replace(/\"/g, "")
					that.temperature=JSON.stringify(data.temperature.data).replace(/\"/g, "")
					that.winddirection=JSON.stringify(data.winddirection.data).replace(/\"/g, "")
					that.windpower=JSON.stringify(data.windpower.data).replace(/\"/g, "")
					that.humidity=JSON.stringify(data.humidity.data).replace(/\"/g, "")
					that.reporttime=JSON.stringify(data.liveData.reporttime).replace(/\"/g, "")
					that.province=JSON.stringify(data.liveData.province).replace(/\"/g, "")
				  },
				  fail: function(info){
					//失败回调
					console.log(info)
				  }
				})
			}
		}
	}
	
</script>

<style scoped>
	page{
		background: #F40 url(../../static/weather.jpg) no-repeat;
	}
	.head{
		display: flex;
		justify-content: space-between;
		background: #f40;
		color: #fff;
		padding: 10upx;
		font-size: 28upx;
	}
	.locate {
		width: 23upx;
		height: 30upx;
		margin-right: 11upx;
		margin-left: 20upx;
	}
	.weather{
		margin-left: 30upx;
		margin-right: 30upx;
	}
	.content{
		/* #ifdef APP-PLUS */
		background: #007AFF;
		/* #endif */
		
		width: 100%;
		height: 100%;
		color: #fff;
	}
	.text{
		padding: 81upx;
		
	}
</style>
