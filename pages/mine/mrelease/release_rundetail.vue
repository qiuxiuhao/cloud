<template>
	<view>
		<!--商品详情-->
		<view class="image1">
			<image :src="good.avatar" class="image2"></image>
		</view>
		<view class="detailview">
			<text class="nametext">{{good.name}}</text><br>
			<text class="pricetext">￥：{{good.price}}</text><br>
			<text class="timetext">{{good.date}}</text><br>
			<text class="detailtext">{{good.detail}}</text>
		</view>
		<view class="jiesuan">
			<button class="button1" v-if="good.status===1">已接取,无法取消</button>
			<button class="button1" v-if="good.status!==1" @click="del">取消发布</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				userinfo:{},
				good:{
					userid:'123457',
					name:'商品1',
					price:50,
					time:'2022-10-26 18:12:59',
					status:0,
					detail:"vue是一套用于构建用户界面的渐进式框架，使用Vue,可以完全在浏览器渲染页面，服务端只提供数据，可以非常方便的构建单页面应用"
				},
				good_id:'',
				good_type:'代办',
			}
		},
		//接受上一个页面的传参
		onLoad(option) {
			this.good_id = option.id
		},
		//初始化数据
		onShow() {
			//从本地获取用户id
			this.userinfo = uni.getStorageSync('userinfo')
			//向数据库获详情
			/*uni.request({
				url:'http://qiuxiuhao.viphk.91tunnel.com/commission_id',
				data:{id:this.good_id,type:this.good_type},
				success:res=> {
					this.good = res.data
					console.log(this.good)
				}
			})*/
		},
		methods: {
			//联系
			talk(){
				uni.navigateTo({
					url:'/pages/messsge_detail/messsge_detail?id=' + this.good.userid
				})
			},
		}
	}
</script>

<style>
	.image1{
		width: 100%;height: 200px;
		border-bottom: solid #ededed 2px;
	}
	.image2{
		width: 100%;height: 200px;
	}
	.detailview{
		padding: 10px;
	}
	.nametext{
		padding-top: 10px;
		font-size: 24px;
	}
	.pricetext{
		padding-top: 10px;
		font-size: 20px;color: red;
	}
	.timetext{
		padding-top: 10px;
		font-size: 12px;
	}
	.detailtext{
		padding-top: 10px;
		font-size: 16px;
	}
	.contact{
		position: absolute;bottom: 102px;left: 0px;
		padding-left: 20px;
		height: 90px;
	}
	.image3{
		height: 40px;width: 40px;
	}
	.jiesuan{
		position: absolute;bottom: 0px;left: 0px;
		padding-top: 20px;
		width: 100%;height: 80px;
		border-top: solid #ededed 2px;
		display: flex;
		flex-direction: row;
	}
	.button1{
		width: 150px;height: 50px;
		background-color: skyblue;color: white;
	}
	.text3{
		font-size: 12px;
	}
</style>
