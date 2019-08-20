<template>
  <div id="show">
		<div class="banner">
			<mt-swipe :auto="3000">
			  <mt-swipe-item v-for="(item,index) in [1,2,3,4]" :key="index">
			    <img :src="showData.bannerImg+item+'.jpg' " />
			  </mt-swipe-item>
			</mt-swipe>
		</div>
		<div v-if="isShowDate">
			<div class="n_ame"><h1>{{showInfo.Name}}</h1></div>
			<div class="xin"><span>新</span></div>
			<div class="tian">
				<div class="one">甜度</div>
				<img :src="`https://res.bestcake.com/m-images/ww/jz/tiandu_${showInfo.Sweet||showInfo.CakeType[0].Sweet}.png`"/>
			</div>
			<div class="yuanwei">
				<div class="one">原味</div>
				<div class="two">{{showInfo.CategoryName}}</div>
			</div>
			<div class="cailiao">
				<div class="one">原材料</div>
				<div class="two">{{showInfo.Resource||showTypes[0].Resource}}</div>
			</div>
			<div class="shihe">
				<div class="one">适合人群</div>
				<div class="two">所有人群</div>
			</div>
			<div class="baoxian">
				<div class="one">保鲜条件</div>
				<div class="two">{{showInfo.KeepFresh||'-'}}</div>
			</div>
		</div>
		<div>
			<img src="../../assets/111.png" style="width: 100%;"/>
		</div>
		<div class="content" v-if="isShowDate">
			<button v-for="(item,index) in showTypes" 
			:key="index" 
			@click="selSize(item,index)" :class="{asd:index==sizeNum}">{{item.Size}}</button>
		</div>
		<div>
			<img src="../../assets/222.png" style="width: 100%;"/>
		</div>
		<div class="sp">
			<div class="shuliang">购买数量</div>
			<div class="anliu">
				<button @click="dev()">-</button>
				{{num}}
				<button @click="num++">+</button>
			</div>
			
		</div>
		<div class="jieshao">
			<div class="j_1">
				<div class="huaxian1">划线价格</div>
				<div class="huaxian2">商品的专柜价、吊牌价、正品零售价、厂商指导价或该商品的曾经展示过的销售价等，并非原价，仅供参考。 </div>
			</div>
			<div class="j_1">
				<div class="huaxian1">未划线价格</div>
				<div class="huaxian2">商品的实时标价，不因表述的差异改变性质。具体成交价格根据商品参加活动，或会员使用优惠券、积分等发生变化，最终以订单结算页价格为准。 </div>
			</div>
		</div>
		<div class="f_box">
			<div class="priceall">¥{{num*showSize.CurrentPrice}}.00</div>
			
			<div class="goumai">立即购买</div>
			<div class="jiaru" @click="addCart">加入购物车</div>
		</div>
	</div>
</template>

<script>
	import { MessageBox } from "mint-ui";
export default {
  data () {
    return {
     showData:{},
		 routeData:{},
		 initData:"",
		 showInfo:{},
		 showTypes:[],
		 isShowDate:false,
		 showSize:{},
		 num:1,
		 sizeNum:0
		 
    }
  },
	created(){
		this.routeData=this.$route.query;
		this.Urlimg=this.routeData.bannerImg+"1.jpg"
		this.pageInit();
	},
	methods:{
		dev(){
			
			if(this.num=="1"){
				
				return;
				}
				this.num--;
			},
		pageInit(){
			this.showData.bannerImg=this.setImg(this.routeData.SupplyNo)
		},
		setImg(No){
			let path="https://res.bestcake.com/m-images";
			if(No.indexOf("KSK")!=-1){
				let data = {
				  City: this.routeData.City,
				  ProName: this.routeData.Name,
				  c: "Product",
				  m: "GetCakeByName",
				  v: new Date().getTime()
				};
				this._getShowData(data,res=>{
					console.log(res);
					this.initData=res;
				})
				return (
					path+`/jd-detail/${this.routeData.Name}/${this.routeData.Name}-`
				);
			}else if(No.indexOf("NS")!=-1){
				let data = {
				  Name: this.routeData.Name,
				  c: "NsCakeCenter",
				  m: "GetNSCakeByName",
				  v: new Date().getTime()
				};
				this._getShowData(data, res => {
				  console.log(res);
				    this.initData=res;
				});
					return (
						path+`/ns-detail/${this.routeData.Name}/${this.routeData.Name}-`
					);
			}else if(No.indexOf("JZ")!=-1){
				let data = {
				  City: this.routeData.City,
				  ProName: this.routeData.Name,
				  c: "IndexCenter",
				  m: "GetjzCakeInfo",
				  v: new Date().getTime()
				};
				this._getShowData(data, res => {
				  // console.log(res);
				    this.initData=res;
				});
					return (
						path+`/jz-detail/${this.routeData.Name}/${this.routeData.Name}-`
					);
			}else if(No.indexOf("RP")!=-1){
				let data = {
				  Name: this.routeData.Name,
				  c: "NsCakeCenter",
				  m: "GetRuPCakeByName",
				  v: new Date().getTime()
				};
				 this._getShowData(data, res => {
				  console.log(res);
				    this.initData=res;
				});
					return (
						path+`/rp-detail/${this.routeData.Name}/${this.routeData.Name}-`
					);
			}
		},
		selSize(item,num){
			this.showSize=item;
			this.sizeNum=num;
		},
		addCart(){
			
			MessageBox.confirm("加入成功,是否是购物车?")
			.then(action=>{
				let temp={
					City:this.$store.state.city,
					SupplyNo:this.$route.query.SupplyNo,
					Name:this.$route.query.Name,
					id:this.showSize.Id,
					CurrentPrice:this.showSize.CurrentPrice,
					Size:this.showSize.Size,
					num:this.num,
					mark:show,
					UrlImg:this.showData.bannerImg+'1.jpg',
					
				}
				
				this.$store.commit("add",temp);
				this.$router.push("/cart")
			}).catch(()=>{
				console.log("no")
			})
			
			
		},
		_getShowData(data,callback){
			this.$apis.getShowData(data).then(res=>{
				callback(res.data.Tag);
			})
			}
		},
		
		
		watch:{
			initData(){
				if(this.initData.length){
					this.initData.map(item=>{
						if(this.routeData.City==item.City){
							this.showTypes.push(item);
						}
						console.log(this.showTypes)
						
					});
					if(this.showTypes.length==0){
						this.showTypes[0]=this.initData[0];
						
					}
					this.showInfo=this.showTypes[0];
					this.isShowDate=true;
					console.log(this.showInfo)
				}else{
					this.showTypes=this.initData.infos.CakeType;
					this.showInfo=this.initData.infos;
					
					this.isShowDate=true;
					
					console.log(this.showInfo)
				}
				this.selSize(this.showTypes[0],0)
			}
		}
	
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
#show {
  .banner {
    height: r(355);
    img {
      width: 100%;
      height: auto;
    }
  }
	.n_ame{
		height: r(40);
		text-align: center;
		font-size: r(24);
		h1{
			font-weight: 600;
			line-height: r(40);
		}
	}
	.xin{
		height: r(60);
		margin-top: r(10);
		border-bottom: r(10) solid #5A5A5A;
		span{
			
			font-size: r(16);
			padding: r(8);
			background: red;
			color: #FFFFFF;
			border-radius: r(5);
		}
		
	}
	.tian{
		margin-top: r(35);
		height: r(32);
		
		img{
			display: block;
			float: left;
			margin-left: r(18);
			height: r(20);
			
		}
	}
	.one{
		width: r(64);
		float: left;
		// line-height: r(32);
		font-size: r(16);
		color: #666666;
		margin-left: r(10);
	}
	.two{
		float: left;
		color: #000000;
		font-size: r(16);
		width: r(268);
		text-align: -webkit-left;
		margin-left: r(16);
		margin-right: r(16);
	}
	.cailiao,.baoxian{
		
		height: r(80);
	}
	.yuanwei,.shihe{
		
		height: r(50);
	}
	.sp{
		height: r(60);
		.shuliang{
			float: left;
			font-size: r(18);
			margin-left: r(10);
		}
		.anliu{
			float: right;
			margin-right: r(20);
			font-size: r(18);
			button{
				background: none;
				border: none;
				font-size: r(20);
				padding: 0 r(10);
			}
		}
	}
	.jieshao{
		height: r(184);
		padding-top: r(10);
		background: #F6F8FA;
		.j_1{
			    clear: both;
					.huaxian1{
						width: r(64);
						float: left;
						font-size: r(16);
						color: #666666;
						margin-left: r(10);
					}
					.huaxian2{
						float: left;
						color: #000000;
						font-size: r(16);
						width: r(268);
						text-align: -webkit-left;
						margin-left: r(16);
						margin-right: r(16);
					}
		}
		
	}
	.f_box{
		position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 99;
    height: r(55);
		background: #FFFFFF;
		.priceall{
			float: left;
			font-size: r(16);
			color: red;
			line-height: r(55);
			margin-left: r(10);
		}
		.goumai{
			float: right;
			line-height: r(55);
			font-size: r(18);
			// margin-right: r(10);
			background: #007AFF;
			color: #FFFFFF;
			padding: 0 r(5);
		}
		.jiaru{
			float: right;
			line-height: r(55);
			font-size: r(18);
			margin-right: r(10);
		}
	}
	.content{
		height: r(50);
		text-align: left;
		margin-top: r(10);
		button{
			margin-left: r(10);
			border: none;
			font-size: r(14);
		}
	}
	.asd{
		background: #0074D9;
		color: #FFFFFF;
	}
}
</style>
