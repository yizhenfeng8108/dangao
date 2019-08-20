<template>
	<div class="reven">
		<div class="biao">
			<div class="top1">
				<</div> <div class="top2">快速注册
			</div>
			<div class="top3">
				<form>
					<p>
						用户名:<input type="text" name="uname" v-model="uname" />
					</p>
					<p>
						密&nbsp;&nbsp;&nbsp;&nbsp;码:<input type="text" name="upwd" v-model="upwd" />
					</p>
					<p>
						昵&nbsp;&nbsp;&nbsp;&nbsp;称:<input type="text" v-model="name" />
					</p>
					<p>
						<button @click.prevent="edit">立即注册</button>
					</p>
				</form>
			</div>
		</div>
	</div>
</template>

<script>
	export default {

		data() {
			return {
				uname: "",
				upwd: "",
				name: ""
			}
		},

		methods: {
			edit() {
				var temp = {
					username: this.uname,
					password: this.upwd,
					name: this.name
				};
		
				this.$apis.edit(temp).then((res) => {
					console.log("OK111")
					 
					  if (res.data.code == 4000) {
					  	console.log("OK")
					  	  this.$router.push("/login")
					  }

				})

			}
		}

	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
	.reven {
		.biao {
			background: rgba(54, 209, 220, .7);
			color: #FFFFFF;
			width: 100%;
			height: r(667);

			.top1 {
				font-size: r(24);
				text-align: left;
				margin-left: r(10);
				height: r(50);
				line-height: r(50);
			}

			.top2 {
				font-size: r(26);
				text-align: left;
				margin-left: r(10);
			}

			.top3 {
				margin-top: r(70);

				p {
					text-align: left;
					margin-left: r(30);
					margin-bottom: r(20);

					input {
						height: r(30);
						width: r(270);
					}
				}

				button {
					width: r(320);
					background: orangered;
					border: none;
					color: #FFFFFF;
					height: r(50);
					font-size: r(20);
				}
			}
		}



	}
</style>
