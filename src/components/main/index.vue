<template>
	<div id="index">
		<div class="location">
			<div class="float-l">
				<img src="https://res.bestcake.com/images/newIndex/localtion.png" class="locImg float-l locImg2">
				<span class="color3 fs14 float-l locImgr text-over addres" style="font-size: r(16);">上海</span>
				<img src="https://res.bestcake.com/images/newIndex/more.png" class="locEnt float-l locImgr">
			</div>
		</div>
		<div class="banner">
			<mt-swipe :auto="4000">
				<mt-swipe-item v-for="(item,index) in SwiperBannerList" :key="index">
					<img :src="item.ImgUrl" />
				</mt-swipe-item>
				
			</mt-swipe>
		</div>
		<div class="nav">
			<img src="https://res.bestcake.com/images/newIndex/title.png?v=1" class="title" style="width: 100%;">
		</div>
		<img class="guanggaoImg" data-src="https://res.bestcake.com/images/newindex/tusi.gif" src="https://res.bestcake.com/images/newindex/tusi.gif" lazy="loaded">
		<div class="iconList">
				<div class="cost">
					<ul>
					  <li v-for="(item,index) in TopIconList" :key="index">
					    <img :src="item.ImgUrl" />
					    <span v-text="item.ActName"></span>
					  </li>
					</ul>
				</div>
		</div>
		<div class="contentList">
				<ul>
					<li v-for="(item,index) in CenterContentList" :key="index">
							<img :src="item.ImgUrl" style="width: 100%;height:auto;"/>
					</li>
				</ul>
		</div>
		
		<div class="broadcast">
			<div class="bro">通知</div>
			<div class="bri">
				<div class="bri_1">贝思客官方申明：我司近期发现有客户通过非正常渠道售卖的代金卡无法正常使用，目前我司正通过法律途径解决此问题。我司在此郑重申明，从未授权过任何渠道售卖我司代金卡，请客户通过正常渠道（如：官网、公司销售）进行购买消费。​</div>
			</div>
		</div>
		<div>
			<div class="box-header"><img class="box-header-img" src="https://res.bestcake.com/m-images/HotRecommend/571060506020139900.jpg" lazy="loaded"></div>
			<swiper_t v-if="SaleList.length!=0">
			  <div class="swiper-slide" v-for="(item,index) in SaleList[0]" :key="index" @click="topath(item)">
			    <img :src="item.ImgUrl" style="width: 100%;height:auto;" alt />
					<h1>{{item.Name}}</h1>
					<div style="color: red;">¥{{item.Price}}<span style="color: #666666;">/{{item.Size}}</span></div>
			  </div>
			</swiper_t>
		</div>
		<div>
			<div class="box-header"><img class="box-header-img seturl" src="https://res.bestcake.com/m-images/HotRecommend/427276281583982800.jpg"></div>
			<swiper_t v-if="SaleList.length!=0">
			  <div class="swiper-slide" v-for="(item,index) in SaleList[1]" :key="index" @click="topath(item)">
			    <img :src="item.ImgUrl" style="width: 100%;height:auto;" alt />
					<h1>{{item.Name}}</h1>
					<div style="color: red;">¥{{item.Price}}<span style="color: #666666;">/{{item.Size}}</span></div>
			  </div>
			</swiper_t>
		</div>
		<div>
			<div class="box-header"><img class="box-header-img seturl" src="https://res.bestcake.com/m-images/HotRecommend/497197919096789000.jpg"></div>
			<swiper_t v-if="SaleList.length!=0">
			  <div class="swiper-slide" v-for="(item,index) in SaleList[2]" :key="index" @click="topath(item)">
			    <img :src="item.ImgUrl" style="width: 100%;height:auto;" alt />
					<h1>{{item.Name}}</h1>
					<div style="color: red;">¥{{item.Price}}<span style="color: #666666;">/{{item.Size}}</span></div>
			  </div>
			</swiper_t>
		</div>
		<div style="height: 2.125rem;width: 100%;"></div>
		
	</div>
	
	
</template>
<script>
	export default {
		data() {
			return {
				topic: [],
				SwiperBannerList: [],
				TopIconList:[],
				CenterContentList:[],
				SaleList:[]
			};
		},
		computed: {
			isTopic() {
				return this.$store.state.isTopic;
			}
		},
		mounted() {
			this.pageInit()
		},
		methods: {
			pageInit() {
				this._getIndexData((res) => {
					console.log(res)
					this.SwiperBannerList = res.SwiperBannerList;
					this.TopIconList=res.TopIconList;
					this.CenterContentList=res.CenterContentList;
					res.SaleList.map(item=>{
						this.SaleList.push(JSON.parse(item.CakeList))
					});
					this.SaleList.map(item=>{
						item.map(item=>{
							item.ImgUrl=this.$global.setUrl(item)
						})
					})
				})
			},
			topath(item){
				this.$router.push({
					path:"show",
					query:{
						City:this.$store.state.city,
						SupplyNo:item.SupplyNo,
						Name:item.Name,
						id:item.Id
					}
				});
			},
			_getIndexData(callback) {
				//首页数据
				this.$apis.getIndexData().then((res) => {
					callback(res.data.Tag.mainresult)
				})
			}
		}
		
	};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
	
	#index{
		
		.location{
			height: r(47);
			width: r(366);
			margin: 0 auto;
			overflow:hidden;
			.float-l{
				float: left;
				.locImg2{
					width: r(20);
				}
				.locImg{
					height: r(23.5);
					margin-top: r(12);
				}
				.locImgr{
					margin-left: r(4);
				}
				.locEnt{
					width: r(9.5);
					height: r(17);
					margin-top: r(17);
				}
				.addres{
					margin-top: r(19);
				}
			}
			
		}
		.banner{
			padding: r(10);
			height: r(180);
			// border: 1px solid red;
			border-radius: r(15);
			overflow: hidden;
			img{
				width: 100%;
				height: aotu;
			}
		}
		.guanggaoImg{
			
			width: 100%;
			height: 100%
		}
		.iconList{
			overflow: hidden;
			padding: r(10);
			.cost{
				li{
					width: r(62);
					height: r(75);
					float: left;
					list-style: none;
					margin: r(10) r(12);
					
					img{
						width: r(52);
						display: block;
						height: r(52);
					}
					
				}
			}
			
		}
		.contentList{
			overflow: hidden;
			padding: r(10);
			li{
				width: r(160);
				height: r(100);
				float: left;
				margin: r(0) r(7);
				// border: 1px solid red;
				// border-radius: 8px;
			}
		}
		.box-header{
			img{
				width: 100%;
				height: auto;
			}
			
		}
		.broadcast{
			height: r(50);
			margin: 0 auto;
			color: #1fb1b8;
			position: relative;
			overflow: hidden;
			border-top: r(5) solid #FAFAFA;
			border-bottom: r(5) solid #FAFAFA;
			font-size: r(16);
			.bro{
				float: left;
				width: r(40);
				height: r(30);
				line-height: r(30);
				text-align: center;
				margin-left: r(10);
				margin-top: r(8);
				background: #1fb1b8;
				border-radius: r(4);
				color: #FFFFFF;
			}
			.bri{
				float: right;
				position: relative;
				margin-right: r(10);
				width: r(294);
				height: 100%;
				top: 0;
				overflow: hidden;
				.bri_1{
					height: r(18);
					line-height: r(18);
					position: absolute;
					top: r(15);
					white-space: nowrap;
					animation: brii 25s linear infinite;
					@keyframes brii{
						from{
							transform: translateX(30%);
						}
						to{
							transform: translate(-100%);
						}
					}
				}
				
			}
			
		}
	}
	
</style>
