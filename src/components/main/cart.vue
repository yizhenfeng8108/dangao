<template>
	<div class="cart">

		<div v-for="(item,index) in cartList" :key="index" class="cartit">
			<div class="chbo">
				<input type="checkbox" v-model="item.bool" @change="count" />
			</div>
			<div class="simg">
				<a>
					<img :src="item.UrlImg" />
				</a>

			</div>
			<div class="rig">
				<div class="rig_t">{{item.Name}}</div>
				<div class="rig_c">
					<div class="rc_l">{{item.Size}}</div>
					<div class="rc_r">
						<button @click="jian(item)">-</button>
						{{item.num}}
						<button @click="add(item)">+</button>
					</div>
				</div>
				<div class="rig_b">￥{{item.CurrentPrice*item.num}}</div>
			</div>
			<div class="huodong">
				优惠方式<span>不参与活动</span>
			</div>
			
		</div>
		
		<div class="zimu">
			<div class="zimu1">Hot&nbspRecommend</div>
			<div class="zimu2"></div>
			<div class="zimu3">热销新品推荐</div>
		</div>
		<div class="img">
			<img src="../../assets/333.png" />
		</div>

		<div class="dibu">
			<div class="dibu1" @click="allsel">
				<input type="checkbox" v-model="isAllsel" />
				<span>全选</span>
			</div>
			<div class="dibu2" @click="del">
				<span>清空</span>
			</div>
			<div class="dibu3">
				合计:<span>{{allPrice}}</span>
			</div>
			<div class="dibu4">
				<button>结算</button>
			</div>
		</div>
	</div>
</template>

<script>
	import {
		MessageBox
	} from "mint-ui";
	export default {
		data() {
			return {
				cartList: [],
				allPrice: 0,
				isAllsel: false,
				isArr: []
			};
		},
		created() {
			this.cartList = this.$store.state.cartList;
			this.cartList.map(item => {
				item.bool = false;
			})
			console.log(this.cartList)

		},
		methods: {
			add(item) {
				this.$store.commit("add", item);
				this.count();
			},
			jian(item) {
				if (item.num <= 1) {
					MessageBox.confirm("确定要删除吗").then(action => {
						this.cartList.map((el, i) => {
							if (el.id == item.id) {
								
								this.cartList.splice(i, 1);
							}
						});

						return;
					});
				}
				item.num--;
				this.count();
			},
			del() {
				this.cartList.splice(0, this.cartList.length);
				this.allPrice = 0;
			},
			count() {

				this.allPrice = 0;

				this.isArr = [];
				this.cartList.map(item => {
					if (item.bool) {
						this.allPrice += item.num * item.CurrentPrice;
						this.isArr.push(item);
					}
				});
				if (this.isArr.length == this.cartList.length) {
					this.isAllsel = true;
				} else {
					this.isAllsel = false;
				}
			},
			allsel() {
				this.isAllsel = !this.isAllsel;
				this.cartList.forEach(item => {
					item.bool = this.isAllsel;
				});
				this.count();
			}
		},
		watch: {
			cartList() {
				console.log("ok")
			}
		}
	};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
	.cart {
		.cartit {
			height: r(136);
			margin-top: r(20);
			border-bottom: r(3) solid #666666;

			.chbo {
				float: left;
				width: r(60);
				height: r(110);

				input {
					margin-top: r(50);
				}
			}

			.simg {
				width: r(110);
				float: left;

				img {
					width: 100%;
					height: r(110);
				}
			}

			.rig {
				float: left;
				margin-left: r(15);
				width: r(180);

				.rig_t {
					font-size: r(18);
					text-align: left;
				}

				.rig_c {
					font-size: r(12);
					color: #666666;
					text-align: left;
					margin-top: r(8);
					height: r(35);

					.rc_l {
						float: left;
						margin-top: r(5);
					}

					.rc_r {
						float: right;
					}
				}
				

				.rig_b {
					font-size: r(18);
					text-align: left;
				}
			}
			.huodong{
				float: left;
				color: red;
				margin-top: r(10);
				span{
					color: #666666;
				}
			}
		}

		.zimu {
			padding-top: r(50);

			.zimu1 {
				line-height: r(35);
				color: #333;
				font-weight: bold;
				font-size: r(22);
			}

			.zimu2 {
				width: r(200);
				height: r(2);
				background: #333;
				margin-left: r(90);
			}

			.zimu3 {
				line-height: r(30);
				color: #333;
				font-weight: bold;
				font-size: r(16);
			}
		}

		.img {
			margin-bottom: r(150);
		}

		.dibu {
			height: r(60);
			position: fixed;
			bottom: r(50);
			// z-index: 90;
			background: #FFFFFF;
			width: 100%;

			.dibu1 {
				float: left;

				input {
					margin-top: r(20);
				}
			}

			.dibu2 {
				float: left;
				width: r(40);
				margin-left: r(20);

				span {
					line-height: r(57);
				}
			}

			.dibu3 {
				float: left;
				margin-left: r(90);
				line-height: r(57);

				span {
					font-size: r(18);
					color: red;
				}
			}

			.dibu4 {
				float: right;
				line-height: r(57);

				button {
					background: blue;
					border: none;
					color: #FFFFFF;
					line-height: r(57);
					width: r(100);
					font-size: r(18);
				}

			}
		}

	}
</style>
