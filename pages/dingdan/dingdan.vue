<template>
	<view class="box flex justify-center align-center" style="height:100vh">
		<!-- 退出登录弹出框 -->
		<uni-popup ref="popup " type="center">
			<view class="bg-white" style="width:430px; height:280px; ">
				<view class="flex align-center" style="font-size:20px; font-weight:600; background-color: #f0f0f0; color:#01cba3; height:55px; padding:0 10px;">
					<text class="iconfont" style="margin-right:6px; font-size:25px;">&#xe661;</text>
					<text>提示</text>
				</view>
				<view class="mt-60 text-center" style="font-size:20px; font-weight:600; color:#01cba3;">
					<text>是否确认提出登录?</text>
				</view>
				
				<view class="logoutbtns flex justify-center">
					<button style="background-color: #01CBA3; width:">确定</button>
					<button>取消</button>
				</view>
			</view>
			
		</uni-popup>
		
		<!-- 页面主体 -->
		<view class="main  relative">
			<!-- 退出登录按钮 -->
			<view class="absolute" style="top:25px; right:22px; " @click="logout">
				<text class="iconfont" style="font-size:30px; color:red;">&#xe81a;</text>
			</view>
			<!-- 菜单 -->
			<view class="flex  list">
				<view :class="dingdansence ? 'active': ''" @click="dingdan"><text>订单列表</text></view>
				<view :class="dingdansence ? '': 'active'" @click="yanshou"><text>确认验收</text></view>
			</view>
			
			<view class="" style="margin-top:37px;">
				<!-- 订单页面 -->
				<view class="dingdan" v-if="dingdansence">
					<view class="flex  align-center text-color-main dingdantitle border-box" style="font-size:18px; font-weight:600; padding:0 75px;" >
						<text>订单编号</text>
						<text>订单名称</text>
						<text>下单人</text>
						<text>下单时间 </text>
						<text>操作</text>
					</view>
					<view class="listItem" style="margin-top:16px; border-radius:14px;" v-for="(item,index) in list">
						<view class="listItem  flex  align-center border-box " style="height:45px; padding:0 0 0 75px;">
							<text class="">{{item.title.bianhao}}</text>
							<text class="">{{item.title.name}}</text>
							<text class="">{{item.title.person}}</text>
							<text class="">{{item.title.time}}</text>
							<text class="flex align-center" style="color:#33d5b5;" @click="showDetail(index)">
								<text>详情</text> 
								<text style="font-size:10px; margin-left:6px; font-weight:600" class="iconfont">&#xe6cc;</text>
							</text>
						</view>
						<view v-show="item.title.open">
							<view  class="listItem  flex  align-center border-box" style="height:45px; padding:0 0 0 75px; font-weight:600; color:#086c58">
								<text class="">图片</text>
								<text class="">名称</text>
								<text class="">单价</text>
								<text class="">
									<text style="margin-right: 28px;">重量</text>
									<text>验收重量</text>
								</text>
								<text class="">
									<text style="margin-right: 28px;">金额</text>
									<text>验收金额</text>
								</text>
							</view>
							
							<view v-for="(item2,index2) in item.items" :class="['listItem',  'flex ', 'align-center' , ' border-box', item2.hot?'hot':'', item2.green?'green':'']" style="height:45px; padding:0 0 0 75px; margin-top:7px;">
								<view class="" style="width:256px;">
									<image :src="item2.img" mode="left" class=""></image>
								</view>
								<text class="">{{item2.name}}</text>
								<text>{{item2.danjia}}</text>
								<text class="">
									<text style="margin-right: 28px;">{{item2.zhongliang}}</text>
									<text>{{item2.yanshouzhongliang}}</text>
								</text>
								<text class="">
									<text style="margin-right: 28px;">{{item2.jine}}</text>
									<text>{{item2.yanshoujine}}</text>
									<text v-if="item2.hot" style="font-weight:600; margin-left:6px;">!</text>
									<text v-if="item2.green" class="iconfont" style="font-weight:600; margin-left:6px;">√</text>
								</text>
							</view>
							
							<view class="mt-20" style="width:1254px; border-top:1px solid #ccc;"></view>
							
							<view class="flex yanshoubtn">
								<button class="active">继续验收</button>
								<button>验收完成</button>
							</view>
						</view>
					</view>
				</view>
				
				<!-- 验收页面 -->
				<view class="yanshou" v-if="!dingdansence">
					<view class="flex justify-between" style="padding-right:60px;">
						
						<view class="flex flex-column" style="width:936px;">
							
							<uni-grid :column="3"  :showBorder="false">
								
							    <uni-grid-item class="" v-for="i in 3">
									
									<view class="relative" style="overflow: hidden; padding:10px 0 23px 0; margin:0 8px;  border:1px solid #ccc;  border-radius:9px;">
										<view class="flex justify-center flex-column" style=" ">
											<view class="flex  justify-center" style="height:190px;">
												<image style="display:block; width:182px; height:155px;" src="../../static/app1.jpg" mode=""></image>
											</view>
											<text class="text  text-center" style="font-size:32px;">红星苹果</text>
											<view class="text  mt-10 text-center">
												<text  style="font-size:32px;">￥6.59 </text>
												<text style="font-size:22px; color:#888;">/500g</text>
											</view>
											
											<view class="absolute  text-center" style="top:-10px; left:-80px; ;width:200px; height:60px;background-color: #01CBA3; transform: rotate(-45deg);">
												<text style="font-size:22px;color:white; line-height:78px;">90%</text>
											</view>
										</view>
									</view>
									
							    </uni-grid-item>
							</uni-grid>
							
							<uni-grid :column="3" class="mt-20" :square="false" style="height:150px;" :showBorder="false" >
							    <uni-grid-item class="" v-for="i in 3">
									
									<view class="relative " style="height:150px; overflow:hidden; margin:0 8px;  border:1px solid #ccc;  border-radius:9px;">
										<view class=" flex align-center justify-around" style="height:150px;">
											
											<view class=" mt30">
												<image src="../../static/app2.jpg" style="width:135px;height:80px;"></image>
											</view>
											
											<view class="flex flex-column justify-around " style="height:150px">
												<view>
													<text class="text  text-center" style="font-size:18px;">红肉苹果</text>
												</view>
												<view >
													<text style="font-size:16px;">￥7.49</text>
													<text style="font-size:11px; color:#888;">/500g</text>
												</view>
											</view>
										</view>
										
										<view class="absolute  text-center" style="top:-20px; left:-90px; ;width:200px; height:54px;background-color: #01CBA3; transform: rotate(-45deg);">
											<text style="font-size:16px;color:white; line-height:78px;">90%</text>
										</view>
									</view>
									
							    </uni-grid-item>
							</uni-grid>
						</view>
						<!-- 奶油苹果 -->
						<view class="flex-1 bdc align-center" style="border-radius:10px; margin-right:80px; overflow:hidden;">
							<view class="flex align-center" style="margin-top:-3px;">
								<image style="width:290x; height:270px;" src="../../static/app3.jpg" mode="top"></image>
							</view>
							<view class="text-center mt-50">
								<text class="text  text-center" style="font-size:32px;">红星苹果</text>
							</view>
							<view class="text  mt-10 text-center mt-30">
								<text  style="font-size:32px;">￥6.59 </text>
								<text style="font-size:22px; color:#888;">/500g</text>
							</view>
						</view>
					</view>
					
					<!-- 记重确认 -->
					<view class="flex  justify-between align-center" style="padding:0 140px 0 10px;">
						
						<view class="ileft " >
							<view class=" flex justify-between tit" style="font-size:25px;width:590px; padding:16px 0; color:#888; ">
								<text>记重</text>
								<text style="color:#444;">11.526kg</text>
							</view>
							<view class=" flex justify-between tit" style="font-size:25px;width:590px; padding:16px 0; color:#888;">
								<text>合计</text>
								<text style="color:red; font-weight: 600;font-size:28px">￥255.86</text>
							</view>
						</view>
						
						<view class="iright mt-30">
							<view class=" flex flex-column align-center  mt-10 justify-center">
								<button class="text-white"  style="width:580px; height:85px; font-size:46px; background-color: #31c3a6; line-height:85px; border-radius: 70px;">确定</button>
								<view class="text-center">
									<text style="font-size:26px; color:#31c3a6" @click="gosearch">没有找到,手动检索</text>
								</view>
							</view>
						</view>
						
						
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
				dingdansence:true,
				list:[
					{	
						title:{
							bianhao:"123135532135",
							name:"11.29大食堂采购",
							person:"刘媛萍",
							time:"2021-11-24 12:36:25",
							open:false
						},
						items:[
							{
								img:"../../static/app.jpg",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"../../static/app.jpg",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192",
								hot:true
							},
							{
							img:"../../static/app.jpg",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								hot:true,
								zhongliang:"32kg",
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"../../static/app.jpg",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								green:true,
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"../../static/app.jpg",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								green:true,
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"../../static/app.jpg",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"../../static/app.jpg",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								green:true,
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							}
						]	
					},
					{
						title:{
							bianhao:"123135532135",
							name:"11.29大食堂采购",
							person:"刘媛萍",
							time:"2021-11-24 12:36:25",
							open:false
						},
						items:[
							{
								img:"../../static/app.jpg",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"../../static/app.jpg",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192",
								hot:true
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								hot:true,
								zhongliang:"32kg",
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								green:true,
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								green:true,
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								green:true,
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							}
						]	
					},
					{
						title:{
							bianhao:"123135532135",
							name:"11.29大食堂采购",
							person:"刘媛萍",
							time:"2021-11-24 12:36:25",
							open:false
						},
						items:[
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192",
								hot:true
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								hot:true,
								zhongliang:"32kg",
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								green:true,
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								green:true,
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								green:true,
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							}
						]	
					},
					{
						title:{
							bianhao:"123135532135",
							name:"11.29大食堂采购",
							person:"刘媛萍",
							time:"2021-11-24 12:36:25",
							open:false
						},
						items:[
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192",
								hot:true
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								hot:true,
								zhongliang:"32kg",
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								green:true,
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								green:true,
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								green:true,
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							}
						]	
					},
					{
						title:{
							bianhao:"123135532135",
							name:"11.29大食堂采购",
							person:"刘媛萍",
							time:"2021-11-24 12:36:25",
							open:false
						},
						items:[
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192",
								hot:true
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								hot:true,
								zhongliang:"32kg",
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								green:true,
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								green:true,
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							},
							{
								img:"",
								name:"新鲜大水果",
								danjia:"￥8/kg",
								zhongliang:"32kg",
								green:true,
								yanshouzhongliang:"32kg",
								jine:"￥192",
								yanshoujine:"￥192"
							}
						]	
					}
				]
			}
		},
		methods: {
			dingdan(){
				this.dingdansence=true
			},
			yanshou(){
				this.dingdansence = false
			},
			showDetail(index){
				for(let i=0; i<this.list.length; i++){
					if(i == index){
						this.list[i].title.open = !this.list[i].title.open
					}else{
						this.list[i].title.open=false;
					}
				}
			},
			logout(){
				 this.$refs.popup.open('center')
			},
			gosearch(){
				uni.navigateTo({
					url:'../search/search'
				})
			}
		}
	}
</script>

<style>
.main{
	width:1366px;
	/* height:768px; */
	padding-left:56px;
	padding-top:17px;
	padding-bottom:40px;
	background-color: rgb(245,245,245);
}
.list{
	border-radius:8px;
	width:260px;
	border:1px solid #1eb698;
}
.list view{
	width:136px;
	height:44px;
	text-align: center;
	line-height:44px;
	color:#1eb698;
}
.dingdan{
	background-color: rgb(245,245,245);
}
.list .active{
	background-color: #1eb698; 
	color:white;
}
.dingdantitle text{
	display:block;
	width:256px;
}

.dingdantitle text:last-of-type{
	width:140px;
}
.listItem{
	background-color: #f3fbfa;
	width:1255px;
	overflow: hidden;
}
.listItem text{
	width:256px;
}
.listItem text:last-of-type{
	width:130px;
}
.hot{
	color:red;
}
.green{
	color:#2ac735;
}
.yanshoubtn{
	display: flex;
	flex-direction: row;
	justify-content:flex-end;
	margin-top: 40px;
	margin-bottom: 20px;
}
.yanshoubtn button{
	background-color: #fff;
	width:90px;
	font-size:15px;
	border:1px solid #01cba3;
	margin:0;
	padding:0;
	color: #01cba3;
	height:40px;
	margin-right: 37px;
}
.yanshoubtn .active{
	background-color: #01cba3;
	color:white;
}
.logoutbtns{
	margin-top: 70px;
}
.logoutbtns button{
	width:90px;
	margin:0 15px;
	background-color: #fff;
	border:1px solid #01CBA3;
	font-size:15px;
}
.tit{
}
</style>
