<template>
	<view>
		<view class="serach">
			<input type="text" class="keyinput" placeholder="输入关键词" v-model="keyword">
		</view>
		<view>
			<view class="" v-for="good in goods">		
				<view v-if="good.type==='失物'" class="item" @click="gotodetail(good.orderId,good.type)">
					<view class="left">
						<img src="" class="imag1">
						<view class="">
							<text class="text1">{{good.name}}</text><br>
							<text class="text2">{{good.time}}</text>
						</view>
					</view>
					<view class="right">
						{{good.type}}<br><text class="text5">{{good.status}}</text>
					</view>
				</view>
				<view v-if="good.type==='招领'" class="item" @click="gotodetail(good.orderId,good.type)">
					<view class="left">
						<img src="" class="imag1">
						<view class="">
							<text class="text1">{{good.name}}</text><br>
							<text class="text2">{{good.time}}</text>
						</view>
					</view>
						<view class="right">
							{{good.type}}<br><text class="text5">{{good.status}}</text>
						</view>
				</view>
				<view v-if="good.type==='代办'" class="item" @click="gotodetail(good.orderId,good.type)">
					<view class="left">
						<img src="" class="imag1">
						<view class="">
							<text class="text1">{{good.name}}</text><br>
							<text class="text2">{{good.time}}</text>
						</view>
					</view>
					<view class="right">
						{{good.type}}<br><text class="text5">{{good.status}}</text>
					</view>
				</view>
				<view v-if="good.type==='二手'" class="item" @click="gotodetail(good.orderId,good.type)">
					<view class="left">
						<img src="" class="imag1">
						<view class="">
							<text class="text1">{{good.name}}</text><br>
							<text class="text2">{{good.time}}</text>
						</view>
					</view>
					<view class="right">
						{{good.type}}<br><text class="text5">{{good.status}}</text>
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
				keyword:'',
				userinfo:{},
				initial_goods:[
				]
			}
		},
		onShow() {
				//从本地获取用户id
				this.userinfo = uni.getStorageSync('userinfo')
				console.log(this.userinfo.id)
				//从数据库获取订单数组
				uni.request({
					url:'http://qiuxiuhao.viphk.91tunnel.com/myorder',
					data:{id:this.userinfo.id},
					success:res=> {
						this.initial_goods = res.data
						console.log(this.initial_goods)
					}
				})
		},
		methods: {
			selectscouce(e){
				this.select.source = this.source[e.detail.value]
			},
			selectstatus(e){
				this.select.status = this.status[e.detail.value]
			},
			gotodetail(id,type){
				uni.navigateTo({
					url:'/pages/mine/order/order_detail?id=' + id +'&type=' +  type
				})
			},
			release(){
				uni.navigateTo({
					url:'/pages/mine/order/release'
				})
			}
		},
		computed:{
			//条件过滤
			goods(){
				return this.initial_goods.filter((p)=>{
					return  p.name.indexOf(this.keyword) !== -1
				})
			}
		}
	}
</script>

<style>
	.select1{
		width: 75%;color: deepskyblue;
		margin-top: 5px;
		margin-left: 10px;
		display: flex;flex-direction: row;
	}
	.select2{
		width: 25%;color: deepskyblue;
		margin-top: 5px;
		margin-left: 10px;
		display: flex;flex-direction: row;
	}
	.serach{
		height: 40px;padding-left: 5%;
		background-color: #66c3E4;align-items: center;
	}
	.keyinput{
		height: 30px;width: 90%;
		background-color: white;
		border: solid;padding-left: 10px;
		border-radius: 5px;
	}	
	.button_1{
		height: 30px;width: 25%;font-size: 14px;
		background-color: deepskyblue;
	}
	.item{
		height: 80px;
		border-bottom: solid #ededed;
		padding: 5px;
		display: flex;flex-direction: row;
		justify-content: space-between;
	}
	.left{
		display: flex;flex-direction: row;
	}
	.imag1{
		width: 60px;height: 60px;
	}
	.right{
		height: 60px;width: 50px;color: skyblue;
	}
	.text1{
		padding-left: 10px;
		font-size: 20px;
	}
	.text2{
		padding-left: 10px;
		font-size: 14px;
	}
	.text5{
		color: red;
	}
</style>
