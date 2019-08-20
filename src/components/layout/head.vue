<template>
  <div id="footer">
			<mt-tabbar v-model="selected" :fixed="true" style="height: 50px;">
			 <mt-tab-item
			   :id="'box'+index"
			   v-for="(item,index) in routerList" 
			   :key="index" 
			   @click.native="sel(index)"
			   :class="{'is-selected':cindex==index}" class="f_box">
			    <i :class="item.className" class="f_i"></i>
			    <span class="f_span">{{item.name}}</span>
			  </mt-tab-item>
			  <div class="shuzi" v-if="this.$store.state.cartList.length==0?false:true">{{$store.getters.count}}</div>
				 
			</mt-tabbar>
  </div>
</template>

<script>
export default {
  data() {
    return {
			selected:"",
      routerList: [
        { path: "/index", name: "首页",className:"fa fa-bank fa-lg" },
        { path: "/news", name: "分类",className:"fa fa-th-large fa-lg"},
        { path: "/cart", name: "购物车",className:"fa fa-truck fa-lg"},
				{ path: "/my", name: "我的",className:"fa fa-user-o fa-lg"}
      ],
			cindex:0
    };
  },
	methods:{
		sel(index){
			this.cindex=index;
			this.$router.push(this.routerList[index].path)
			}
		}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
ul{
  overflow: hidden;
}
li{
  list-style: none;
  float: left;
  margin-left: 20px;
}

.f_box{
	text-align: center;
	line-height: r(50);
	.f_i{
		font-size: r(20);
		margin-left: r(5);
		margin-top: r(4);
	}
	.f_span{
		display: block;
		margin: r(5) 0 0 r(5);
	}
}
.shuzi{
	width: r(20);
	height: r(20);
	border-radius: 50%;
	background: red;
	color: #fff;
	line-height: r(20);
	font-size: r(14);
	position: absolute;
	right: r(110);
	top:r(-6);
	z-index: 99;
	
}
</style>
