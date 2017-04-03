<template>
    <div id="info" class="page"
    v-show="show"
    :style="{'z-index':zIndex}"
    @mousemove="wave"></div>
</template>

<script>
    export default {
        props:['show'],
        data(){
            return {
                zIndex:90
            }
        },
        methods:{
            wave(ev){
                var width = this.$el.getBoundingClientRect().width;
                var height =this.$el.getBoundingClientRect().height;
                this.$el.style.transform = `
                        rotateX(${(ev.clientY - (height/2))*0.01}deg) rotateY(${-(ev.clientX - (width/2))*0.01}deg)
                `;
            }
        }
    }
</script>

<style lang="less" scoped>
    #info{
        background:greenyellow
    }
</style>