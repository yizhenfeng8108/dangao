<template>
  <div class="swiper-container swiper-container-horizontal swiper-container-3d swiper-container-coverflow"
         style="cursor: grabbing;">
         <div class="swiper-wrapper" style="transform: translate3d(-64px, 0px, 0px); transition-duration: 0ms;">
         <slot>
         </slot>
     </div>
     </div>
</template>

<script>
export default {
  data () {
    return {
     
    }
  },
	mounted(){
		this.pageInit();
	},
	methods:{
		pageInit(){
		    new Swiper('.swiper-container', {
		        pagination: '.swiper-pagination',
		        effect: 'coverflow',
		        grabCursor: true,
		        centeredSlides: true,
		        slidesPerView: '3',
		        coverflow: {
		            rotate: 50,
		            stretch: 0,
		            depth: 100,
		            modifier: 1,
		            slideShadows: true
		        }
		    });
		}
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
	.swiper-container{
		height: r(190)
	}
</style>
