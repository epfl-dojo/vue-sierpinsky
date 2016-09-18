<template>
        <polygon :points="points" :style="style" ></polygon>
</template>
<script>
    export default{
        props: ['size', 'pointa', 'pointb', 'pointc', 'style'],
        computed:{
            points(){
                console.log(`${this.pointa} ${this.pointb} ${this.pointc}`);
                return `${this.pointa} ${this.pointb} ${this.pointc}`;
            }
        }
    }
</script>
