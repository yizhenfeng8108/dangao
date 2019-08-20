<template>
  <div class="login">
  		<div class="biao">
  			<div class="top1"><</div>
  			<div class="top2">登录</div>
  			<div class="top3">
  				<form>
  					<p>
  						用户名:<input type="text" name="uname" v-model="uname"/>
  					</p>
  					<p>
  						密&nbsp;&nbsp;&nbsp;&nbsp;码:<input type="text" name="upwd" v-model="upwd"/>
  					</p>
  					
  					<p>
  						<button @click.prevent="login">立即登录</button>
  					</p>
  				</form>
  			</div>
  		</div>
  </div>
</template>

<script>
	import { Tabbar, TabItem ,Toast} from "mint-ui";
import Store from "storejs"
export default {
  
  data () {
    return {
      uname:"",
      upwd:""
    }
  },
  methods:{
      login(){
				this.$apis.login({username:this.uname,password:this.upwd}).then(res=>{
					if(res.data.code==="1000"){
						this.$router.push("/reven");
					}else if(res.data.code==="2000"){
						Store.set("userInfo",res.data.userInfo)
						this.$router.push("/my")
					}else if(res.data.code==="3000"){
						
						Toast(res.data.msg)
					}
				})
			}
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
	.login{
		.biao{
			background: rgba(54,209,220,.7);
			color: #FFFFFF;
			width: 100%;
			height: r(667);
			.top1{
				font-size: r(24);
				text-align: left;
				margin-left: r(10);
				height: r(50);
				line-height: r(50);
			}
			.top2{
				font-size: r(26);
				text-align: left;
				margin-left: r(10);
			}
			.top3{
				margin-top: r(70);
				p{
					text-align: left;
					margin-left: r(30);
					margin-bottom: r(20);
					input{
						height: r(30);
						width: r(270);
					}
				}
				button{
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
