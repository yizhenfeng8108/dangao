<template>
  <div class="goods">
      <ul class="goo_ul">  
        <li v-for="(item,index) in tablist" :key="index" style="float:left">
          <span @click="sel(index)" class="goo_span">{{item.title}}</span>
        </li>
      </ul>
      <div>
        <ul>
          <li v-for="(item,index) in goodList" :key="index" class="list">
            
			<img :src="item.ImgUrl" style="width:100%;height:auto;" @click="topath(item)">
			<div class="ziti"><p style="color: #000000;font-size:0.35rem;">{{item.Name}}</p></div>
			<div class="ziti"><p style="color: #666666;">{{item.Means}}</p></div>
			<span style="color: red;">¥{{item.CurrentPrice}}</span><span style="color: #666666;">/{{item.Size}}</span>
            <button @click="add(item)">购买</button>
          </li>
        </ul>
      </div>
      <div style="height:100px;"></div>
  </div>
</template>
<script>
export default {
  data () {
    return {
        goodList:[]
    }
  },
  props:["tablist"],
  created(){
   this.sel(0);
   
  },  
  methods:{
    sel(index){
      this.goodList=this.tablist[index].list;
			
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
		add(item){
			let temp={
				City:this.$store.state.city,
				SupplyNo:item.SupplyNo,
				Name:item.Name,
				id:item.Id||item.ID,
				CurrentPrice:item.CurrentPrice,
				UrlImg:item.ImgUrl,
				Size:item.Size
			};
			this.$store.commit("add",temp);
		}
  },
  watch:{
    tablist(){
       this.sel(0);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss"> 
.list{ 
  display: inline-block;
  width:49%;
  height:r(100);
}
.goods{
	.goo_ul{
		overflow: hidden;
		.goo_span{
			display: block;
			font-size: r(16);
			height: r(50);
			line-height: r(50);
			margin-left: r(70);
			
		}
	}
}
.ziti{
	width: r(160);
	
	overflow: hidden;
	line-height: r(21);
	white-space: nowrap;
	text-overflow: ellipsis;
}
</style>
