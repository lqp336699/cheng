<template>
	<view class="box ">

		<view class="main flex justify-between relative align-center row-reverse ">
			<!-- 设置 -->
			
			<view class="setting absolute"  @click="open">
				<text class="iconfont" style="font-size:30px; color:#333;">&#xe64b;</text>
			</view>
			
			<!-- 弹出框 -->
			
			<uni-popup ref="popup" type="center" background-color="#fff" >
				
				<!-- 输入管理员密码弹出框 -->
				
				<view class="popsuper relative " v-show="!hasSuperUser" style="height:330px; width:440px; overflow: hidden;">
					<text class="close text-center absolute text-white" style="line-height:24px; border-radius: 50%; height:26px; width:26px; background-color: #b9b6b8; font-size:24px; top:14px; right:20px;" @click="close">×</text>
					<view class="text-center mt-70">
						<text class="text-color-main" style="font-size:23px; font-weight:600">请输入管理员密码</text>
					</view>
					<view class="flex justify-center mt-50">
						<input type="text" class="popinp bd text-center" placeholder="请输入密码" style="border:1px solid #399c88" value="" />
					</view>
					
					<view class="btns flex justify-center align-center mt-70">
						<button class="" style="margin-right: 25px;" @click="superLogin">确认</button>
						<button class="" style="background-color: white; border:1px solid #01CBA3; color:#333;" @click="close">取消</button>
					</view>
				</view>
				
				<!-- 管理员登陆成功后弹出框 -->
				
				<view class="popmain" v-show="hasSuperUser">
					<view class="flex justify-between px-30 align-center" style="height:60px;background-color: #f0f0f0;">
						<text style="color:#399c88; font-size:19px;font-weight:600;">设置</text>
						<text class="text-center text-white" style="line-height:24px; border-radius: 50%; height:26px; width:26px; background-color: #b9b6b8; font-size:24px;" @click="close">×</text>
					</view>
					
					<view class="border-box flex justify-between flex-wrap" style="padding:38px 70px;">
						<view class="flex justify-between align-center " style="width:347px;">
							<text><text style="color:red; margin-right:6px;">*</text>服务器地址：</text>
							<input type="text" class="popinp bd " value="" />
						</view>
						
						<view class="flex justify-between align-center" style="width:340px;">
							<text><text style="color:red; margin-right:6px;">*</text>接口密钥：</text>
							<input type="text" class="popinp bd" value="" />
						</view>
						
						<view class="flex justify-between align-center  mt-20" style="width:347px;">
							<text><text style="color:red; margin-right:6px;">*</text>设备编号：</text>
							<input type="text" class="popinp bd" value="" />
						</view>
					</view>
					
					<view class="btns flex justify-center align-center">
						<button class="" style="margin-right: 25px;" @click="close">确认</button>
						<button class="" style="background-color: white; border:1px solid #01CBA3; color:#333;" @click="close">取消</button>
					</view>
				</view>
				
			</uni-popup>
			
			<!-- 登录框 -->
			
			<view class="login mr-110 relative bg-white border-box px-50">
				<view class="logo absolute ">
					<image src="../../static/logo.png"></image>
				</view>
				<view class="title flex align-start justify-around mt-90">
					<view :class="saoma ? '' : 'text-title'" @click="mimalogin">密码登录</view>
					<view class="huise">|</view>
					<view :class="saoma ? 'text-title' : ''" @click="saomalogin">扫码登录</view>
				</view>
				
				<!-- 扫码登录 -->
				
				<view class="flex justify-center mt-30" 	style=" height:240px;"  v-if="saoma">
					<image style="width:240px; height:240px" src="../../static/ewm.jpg" mode=""></image>
				</view>	
				
				<!-- 密码登录 -->
				<view v-if="!saoma">
					<view class="inps mt-40 font-sm" >
						<input type="text" placeholder="请输入账号" class="user">
						<input type="text" placeholder="请输入密码" class="pass">
					</view>
					<view class="flex justify-between mt-10 align-center" >
						<label class="flex align-center">
							<checkbox value="false" style="transform:scale(0.7)" /><text>记住密码</text>
						</label>
						<text>忘记密码？</text>
					</view>
					<button class="bg-button text-white mt-30">登录</button>
				</view>
				
			</view>
		</view>	
	</view>
</template>

<script>
	export default {
		data() {
			return {
				hasSuperUser:false,
				saoma:false,
			}
		},
		methods: {
			open(){
			        this.$refs.popup.open('center')
			      },
			close(){
				this.$refs.popup.close()			  
			},
			superLogin(){
				this.hasSuperUser = true;
			},
			mimalogin(){
				this.saoma=false;
				console.log('666')
			},
			saomalogin(){
				this.saoma=true;
				console.log('666')
			}
		}
	}
</script>

<style>
	.box{
		height:100vh;
		width:100vw;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.main{
		background: url(../../static/login.jpg) no-repeat;
		height:768px;
		width:1366px;
	}
	.login{
		display: block;
		width:455px;
		height:440px;
		z-index:100;
		border-radius: 14px;
	}
	.logo{
		top:-75px;
		left:153px;
	}
	.logo image{
		height: 150px;
		width: 150px;
	}
	.title{
		
	}
	.inps input{
		height:46px;
		border-radius:8px;
		border:1px solid #ccc;
		text-indent:55px;
		font-size:10px;
	}
	.user{
		background: url('../../static/usericon.png') no-repeat;
		background-size:77px 72px;
		background-position:-14px -7px;
		margin-bottom: 26px;
	}
	.pass{
		background: url('../../static/passicon.png') no-repeat;
		background-size:77px 72px;
		background-position:-14px -8px;
		
	}
	.bg-button{
		height:43px;
		line-height: 43px;
	}
	.setting{
		top:30px;
		left:30px;
	}
	.popmain{
		width:855px;
		height:350px;
		font-size:14px;
		color:#338c7a;
	}
	.popinp{
		width:235px;
		height:35px;
		border:1px solid #28a745;
		border-radius:6px;
	}
	.btns button{
		padding: 0;
		margin: 0;
		display: block;
		width:80px;
		height:40px;
		background-color: #01cba3;
		color:white;
		line-height:40px;
		font-size:15px;
	}
	.close{
		top:15px;
		right:20px;
	}
</style>
