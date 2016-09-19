<template>
	<button @click="depth++">Click to add depth: {{depth}}</button>
	<div>
		<svg :width="size" :height="size">
			<vtriangle :points="fpoints" :style="style1"></vtriangle>
			<template v-for="item in polygons">
				<vtriangle :points="item" :style="style2"></vtriangle>
			</template>
		</svg>
	</div>
	<pre>Sub triangles: {{polygons | json}}</pre>
</template>

<script>
	import vtriangle from "./vtriangle.vue"
	export default {
		data () {
			return {
				depth:0,
				size: 400,
				style1:{
					fill: 'indigo'
				},
				style2:{
					fill: 'royalblue'
				}
			}
		},
		computed: {
			fpoints(){
				return {
					pointa: this.size/2 + "," + 0,
					pointb: this.size + "," + this.size,
					pointc: 0 + "," + this.size
				}
			},
			polygons(){
				return this.generate([], 0, 0, this.size, this.depth);
			}
		},
		methods:{
			generate(stack, x, y, size, depth, next){
				let result = [];
				if(depth > 1) {
					stack.push(...this.generate([], (x + (size/4)), y, size/2, depth-1));
					stack.push(...this.generate([], x, (y + (size/2)), size/2, depth-1));
					stack.push(...this.generate([], (x + (size/2)), (y + (size/2)), size/2, depth-1));
				}
				if(depth > 0){
					stack.push(this.getPoints(x, y, size));
				}
				return stack;
			},
			getPoints(x, y, size){
				var pointa = (x + (size/4)) + "," + (y + (size/2));
				var pointb = (x + (0.75 * size)) + "," + (y + (size/2)); 
				var pointc = (x + (size/2)) + "," + (y + size);
				return { pointa, pointb, pointc };
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