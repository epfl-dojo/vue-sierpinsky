<template>
	<button @click="depth++">{{depth}}</button>
	<div>
		<svg :width="size" :height="size">
			<vtriangle :pointa="pointa" :pointb="pointb" :pointc="pointc" :style="style1"></vtriangle>
			<template v-for="item in polygons">
				<vtriangle :pointa="item.pointa" :pointb="item.pointb" :pointc="item.pointc" :style="style2"></vtriangle>
			</template>
		</svg>
	</div>
	<pre>{{polygons | json}}</pre>
</template>

<script>
import vtriangle from "./vtriangle.vue"

export default {
  data () {
    return {
    	depth:1,
    	size: 400,
    	topX: 0,
    	topY: 0,
			style1:{
				fill: 'lime'
			},
			style2:{
				fill: 'purple'
			}
    }
  },
  computed: {
		pointa(){
			return this.size/2+","+this.topY;
		},
		pointb(){
			return this.size+","+this.size;
		},
		pointc(){
			return this.topX+","+this.size;
		},
	  polygons(){
		  return this.generate([], this.topX, this.topY, this.size, this.depth);
	  }
  },
  methods:{
		generate(stack, x, y, size, depth, next){
			let result = [];
			if(depth > 1) {
				stack.push(...this.generate([], (x + (size/4)), 	y, 								size/2, depth-1))
				stack.push(...this.generate([], x, 							(y + (size/2)), 	size/2, depth-1))
				stack.push(...this.generate([], (x + (size/2)), (y + (size/2)), 	size/2, depth-1))
			}
			stack.push(this.getPoints(x, y, size))
			return stack;
		},
		getPoints(x, y, size){
			var pointa = (x + (size/4)) + "," + (y + (size/2));
			var pointb = (x + (0.75 * size)) + "," + (y + (size / 2)); 
			var pointc = (x + (size / 2)) + "," + (y + size);
			return { pointa, pointb, pointc }
		}
  },
  components: {
		vtriangle
  }
}
</script>
<style>
	svg {
		border: solid 1px #42b983;
	}
</style>