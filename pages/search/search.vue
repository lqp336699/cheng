<template>
	<view class="flex justify-center align-center" style="width: 100vw; height: 100vh;">
		<view class="main border-box">
			<view class="text-center">
				<text style="font-size:50px; font-weight:550;">手动检索</text>
			</view>
			<view class="flex align-center mt-20">
				<input class="text-center" type="text" style="font-size:20px; border:1px solid #31c3a6; width:1110px; height:68px;" placeholder="输入首字母缩写或商品名称" value="" />
				<button class="flex-1 iconfont" style="border-radius:0; height:70px; background-color: #31c3a6; color:white; line-height:70px; font-size:40px; font-weight:600" type="default" >&#xe6b0;</button>
			</view>
			
			<view class="box">
				<scroll-view class="scroll" :show-scrollbar="false" scroll-x="true" >
					<view class="bd">
						<view class="scrollitem"><text>肉禽</text></view>
						<view class="scrollitem"><text>水产</text></view>
						<view class="scrollitem"><text>干货</text></view>
						<view class="scrollitem"><text>米蛋组</text></view>
						<view class="scrollitem"><text>米蛋组</text></view>
						<view class="scrollitem"><text>水产</text></view>
						<view class="scrollitem"><text>水产</text></view>
						<view class="scrollitem"><text>水产</text></view>
						<view class="scrollitem"><text>水产</text></view>
					</view>
				</scroll-view>
			</view>
		</view>
	</view>
		
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style>
.main{
	width:1366px;
	height:768px;
	padding-left:56px;
	padding-right:40px;
	padding-top:17px;
	padding-bottom:40px;
	background-color: rgb(245,245,245);
}
.scroll{
	white-space:nowrap;
	box-sizing:border-box;
	border:1px solid #000;
}
.scrollitem{
	display: inline-block;
	width:200px;
	padding:25px 0;
	font-size:23px;
	color:#333;
}
.box{
	height:80px;
	/* overflow: hidden; */
}
</style>
