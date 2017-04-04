<template>
<transition>
    <div id="hp" class="page"
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
                    switchFinish:true
                },
                val:1,
                val2:2
            }
        },
        methods:{
            //页面鼠标滑过效果
            wave(ev){
                if(!this.status.switchFinish)return
                var width = this.$el.getBoundingClientRect().width;
                var height =this.$el.getBoundingClientRect().height;
                this.$el.style.transform = `
                        rotateX(${(ev.clientY - (height/2))*0.01}deg) rotateY(${-(ev.clientX - (width/2))*0.01}deg)
                `;
            }
        },
        watch:{
            //页面进出效果
            show(){
                console.log(this.show);
                var el = this.$el;
                var that = this;
                this.status.switchFinish = false;
                if(this.show == true){
                    el.style.display = 'block';
                    Velocity(el,{
                        opacity:1,
                        translateX:'0%'
                    },{
                        duration:500,
                        complete(){
                            that.status.switchFinish = true;
                        }
                    })
                }else{
                    Velocity(el,{
                        opacity:0,
                        translateX:'-120%'
                    },{
                        duration:500,
                        complete(){
                            el.style.display = 'none';
                        }
                    });
                }
            }
        }
    }
</script>

<style lang="less" scoped>
    #hp{
        background:#3399CC;
    }
</style>