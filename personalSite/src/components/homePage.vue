<template>
<transition>
    <div id="hp" class="page"
        v-show="show"
        :style="{'z-index':zIndex}"
        @mousemove="wave">
            <h1>这是首页</h1>
        </div>
</transition>
</template>

<script>
    import Velocity from 'velocity-animate';
    export default {
        props:['show'],
        data(){
            return {
                zIndex:100,
                starty:null,
                disy:null,
                status:{
                    isStart:false
                },
                val:1,
                val2:2
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
    #hp{
        background:#3399CC;
    }
</style>