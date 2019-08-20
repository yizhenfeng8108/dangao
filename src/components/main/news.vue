<template>
	
  <div>
			<div class="tou">
				<span @click="sel(1)" class="t_sp">自营</span>
				<span @click="sel(2)" class="t_sp">贝式严选</span>
			</div>
			
			<goodsList v-if="tabData.length!=0" :tablist="tabData"></goodsList>
  </div>
</template>
<script>
import goodsList from "@/components/main/item1"
export default {
  data() {
    return {
			goodsList:[
				{title:"经典",mark:"KSK",list:[]},
				{title:"女神",mark:"NS",list:[]},
				{title:"伴手礼",mark:"JZ",list:[]},
				{title:"乳品",mark:"RP",list:[]}
			],
			tabData:[]
		};
  },
  mounted() {
    this.pageInit();
  },
  // computed:{name(){}},
  components: {
    goodsList
  },
  methods: {
    pageInit(){
			this._getNsCakeCenter(res=>{
				this.goodsList.map((item)=>{
					res.map((it)=>{
						if(it.SupplyNo.indexOf(item.mark)!=-1){
							it.ImgUrl=this.$global.setUrl(it);
							item.list.push(it);
						}
					})
				})
				this.sel(1);
			})
		},
		sel(num){
			var cnum=num;
			if(num==1){
				this.tabData=this.goodsList.slice(0,3);
			}else{
				this.tabData=this.goodsList.slice(3);
			}
		},
		_getNsCakeCenter(callBack){
			this.$apis.getNsCakeCenter().then(res=>{
				console.log(res)
				callBack(res.data.Tag.cakelist);
			})
		}
  }
};
</script>

<style scoped lang="scss">
	.tou{
		height: r(52);
		font-size: r(18);
		border-bottom: 1px solid #d9d9d9;
		.t_sp{
			line-height: r(52);
			text-align: center;
			padding: r(25);
		}
	}
	
	.active{
		color: #1db0b8;
	}
	
</style>