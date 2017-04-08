<template>
    <div id="info" class="page"
    :style="{'z-index':zIndex}"
    @mousemove="wave">
        <infoCard></infoCard>
    </div>
</template>

<script>
import infoCard from './info/infoCard'
    export default {
        components:{infoCard},
        props:['show'],
        data(){
            return {
                zIndex:90,
                status:{
                    switchFinish:true
                },
            }
        },
        methods:{
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
            show(){
                console.log(this.show);
                var el = this.$el;
                var that = this;
                if(this.show == true){
                    el.style.display = 'block';
                    Velocity(el,{
                        opacity:1,
                        translateY:'0%'
                    },{
                        duration:500,
                        complete(){
                            that.status.switchFinish = true;
                        }
                    })
                }else{
                    Velocity(el,{
                        opacity:0,
                        translateY:'-120%'
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
    #info{
        display:none;
        background:url(../assets/infobg.gif);
        position:relative;
    }
</style>