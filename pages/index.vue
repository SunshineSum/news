<template>
	<view>
		<view class="head">
			<image class="locate" src="../static/locate.png" mode="widthFix"></image>
			<view class="adress">
				{{address}}
			</view>
			<view class="weather">
				天气：{{weather}}
			</view>
		</view>
		<view class="" @tap="gotoWeather">
			查看天气状况
		</view>
		<view class="" @tap="gotoNews">
			查看新闻
		</view>
	</view>
</template>

<script>
	import amapFile from '../common/adress/amap-wx.js'
	export default{
		data(){
			return{
				key:'7497c68043d31ea429ca233b876a10f5',
				myAmapFun:null,
				address:'',
				weather:''				
			}
		},
		onLoad() {
			// #ifdef APP-PLUS
			this.myAmapFun = new amapFile.AMapWX({key:this.key});
			// #endif
		    
		},
		onShow() {
			// #ifdef APP-PLUS
			this.getAdress()
			this.weatherFn()
			// #endif
			
		},
		methods:{
			gotoNews(){
				uni.navigateTo({
				    url: './new/new',
				});
			},
			gotoWeather(){
				uni.navigateTo({
				    url: './weather/weather',
				});
			},
			//获取当前位置
			getAdress(){
				var that = this;
				// debugger
				that.address="定位中..."
				that.myAmapFun.getRegeo({
				  success(data){
				    //成功回调
					// console.log(JSON.stringify(data),'adress')
					var addressComponent=data[0].regeocodeData.addressComponent
					// console.log(addressComponent)
					that.address=JSON.stringify(addressComponent.province)+''+
					JSON.stringify(addressComponent.district)+''+
					JSON.stringify(addressComponent.township)+''+
					JSON.stringify(addressComponent.streetNumber.street)+''+
					JSON.stringify(addressComponent.streetNumber.number)
					// console.log(this.address)
					that.address=that.address.replace(/\"/g, "")
				  },
				  fail(info){
				    //失败回调
				    console.log(info)
				  }
				})
			},
			weatherFn(){
				// console.log('111111111')
				var that = this;
				that.myAmapFun.getWeather({
				  success: function(data){
					//成功回调
					console.log(JSON.stringify(data),'weather')
					that.weather=JSON.stringify(data.weather.data).replace(/\"/g, "")
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
	.head{
		display: flex;
		background: #f40;
		color: #fff;
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
	}
</style>
