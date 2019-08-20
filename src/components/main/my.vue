<template>
	<div>
		<div class="touxiang">
			<img src="https://res.bestcake.com/m-images/order/mw-person-tx.png" />
		</div>
		<div class="yonghu">{{userInfo.name}}</div>
		<div class="huiyuan">
			<div class="am-u-sm-3">
				<div class="am-u-sm-12 clplr person-vip-1" align="center">会员等级</div>
				<div class="am-u-sm-12 clplr person-vip-2 ng-binding" align="center">V0</div>
			</div>
			<div class="am-u-sm-3">
				<div class="am-u-sm-12 clplr person-vip-1" align="center">吉致币</div>
				<div class="am-u-sm-12 clplr person-vip-2 ng-binding" align="center">0</div>
			</div>
			<div class="am-u-sm-3">
				<div class="am-u-sm-12 clplr person-vip-1" align="center">优惠券</div>
				<div class="am-u-sm-12 clplr person-vip-2 ng-binding" align="center">0</div>
			</div>
			<div class="am-u-sm-3">
				<div class="am-u-sm-12 clplr person-vip-1" align="center">兑换券</div>
				<div class="am-u-sm-12 clplr person-vip-2 ng-binding" align="center">0</div>
			</div>
		</div>
		<div class="person-dd">
            <div class="person-dd-1">
                <div class="person-dd-2"><img src="https://res.bestcake.com\m-images\order\mw-person-dd.png"></div>
                <div class="person-dd-3">我的订单</div>
                <div class="person-dd-4" style=""><img src="https://res.bestcake.com\m-images\order\mw_firm_right.jpg"></div>
            </div>
            <div class="personclear"></div>
            <div class="person-dd-1">
                <div class="person-dd-2"><img src="https://res.bestcake.com\m-images\order\mw_firm_ad.jpg"></div>
                <div class="person-dd-3">收货地址</div>
                <div class="person-dd-4" style=""><img src="https://res.bestcake.com\m-images\order\mw_firm_right.jpg"></div>
            </div>
           
     </div>
		 <div class="di">
			 <div class="di1">
				 <p>客服热线：400-627-5757</p>
				 <p>服务协议与证照信息</p>
			 </div>
			 <button @click="tui">退出登录</button>
			 
		 </div>

</div>
</template>

<script>
	import Store from "storejs"
	import {
		Tabbar,
		TabItem
	} from "mint-ui";
	export default {

		data() {
			return {
				userInfo: {}
			}
		},
		created() {
			if (Store.get("userInfo")) {
				this.userInfo = Store.get("userInfo");
				console.log(this.userInfo)
			} else {
				this.$router.push("/login");
			}
		},
		methods:{
			tui(){
				Store.remove("userInfo");
				this.$router.push("/login");
			}
		}

	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
	.touxiang {
		padding-top: r(20);

		img {
			width: r(78);
		}
	}

	.yonghu {
		height: r(30);
	}
	.huiyuan{
		padding-top: r(30);
    background: #fff;
    padding-bottom: r(20);
		.am-u-sm-3{
			float: left;
			padding: 0 r(20);
			color: #666666;
			font-size:r(16);
		}
	}
	.person-dd{
		margin-top: r(50);
		width: 100%;
		height: r(100);
		.person-dd-1{
			height: r(40);
			padding-left: r(10);
			border-bottom: r(2) solid #ddd;
			
		}
		.personclear{
			clear: both;
			margin-left: r(10);
		}
		.person-dd-2{
			margin-top: r(5);
			float: left;
			img{
				width: r(15);
			}
		}
		.person-dd-3{
			float: left;
			font-size: r(18);
			line-height: r(32);
			margin-left: r(5);
		}
		.person-dd-4{
			float: right;
			margin-right: r(10);
			margin-top: r(10);
			img{
				width: r(9);
			}
		}
	}
	.di{
		height: r(500);
		background: #fff;
		.di1{
			margin-top: r(100);
			p{
				color: #666666;
				font-size: r(16);
				margin-bottom: r(5);
			}
		}
		button{
			width: r(300);
			height: r(40);
			background: orangered;
			font-size: r(20);
			border: none;
			color: #fff;
			
		}
		
	}
	
</style>
