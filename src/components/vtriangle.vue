<template>
	<polygon :points="pointstring" :style="style" ></polygon>
</template>
<script>
	export default{
		props: ['size', 'points', 'style'],
		computed:{
			pointstring(){
				return `${this.points.pointa} ${this.points.pointb} ${this.points.pointc}`;
			}
		}
	}
</script>
