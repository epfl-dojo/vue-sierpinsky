<template>
        <polygon  v-if="bottom" points="{{pointA}} {{pointB}} {{pointC}}" style="fill:lime;stroke:purple;stroke-width:1" ></polygon>
        <sierpinsky v-if="notBottom" :depth="nextdepth" :x="topSierpinsky.x" :y="topSierpinsky.y" :size="size/2" ></sierpinsky>
        <sierpinsky v-if="notBottom" :depth="nextdepth" :x="bottomRightSierpinsky.x" :y="bottomRightSierpinsky.y" :size="size/2" ></sierpinsky>
        <sierpinsky v-if="notBottom" :depth="nextdepth" :x="bottomLeftSierpinsky.x" :y="bottomLeftSierpinsky.y" :size="size/2" ></sierpinsky>
</template>
<script>

    var sierpinsky;
    sierpinsky = {
        components: {
        },
        props: ['depth', 'size', 'x', 'y'],
        methods: {
            
        },
        computed:{
            topSierpinsky() {
                return {x: 50, y:100}
            },
            bottomRightSierpinsky() {
                return {x: 150, y:100}
            },
            bottomLeftSierpinsky() {
                return {x: 250, y:100}
            },                        
            pointA() {
                var ax, ay;
                ax=this.x;
                ay=this.y+this.size;
                return "" + ax + "," + ay;
            },
            pointB() {
                var ax, ay;
                ax=this.x+this.size;
                ay=this.y+this.size;
                return "" + ax + "," + ay;
            },
            pointC() {
                var ax, ay;
                ax=this.x+(this.size/2);
                ay=this.y;
                return "" + ax + "," + ay;
            },
            bottom(){
                console.log(this.depth);
                return this.depth == 0
            },
            notBottom() {
                return this.depth > 0
            },
            nextdepth(){
                debugger;
                return this.depth -1;
            }
        }
    }
    sierpinsky.components.sierpinsky = sierpinsky;
    export default sierpinsky;
</script>
