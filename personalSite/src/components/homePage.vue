<template>
<transition>
    <div id="hp" class="page"
        :style="{'z-index':zIndex}"
        @mousemove="wave">
        <div class="hp-mask">
            <div class="bd mask-bd-t"></div>
            <div class="bd mask-bd-l"></div>
            <div class="bd mask-bd-r"></div>
            <div class="bd mask-bd-b"></div>
        </div>
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
                this.$el.style.backgroundPosition = `
                        ${50+(ev.clientX - (width/2))*0.0005}% ${50 - (ev.clientY - (height/2))*0.005}%
                `;
            }
        },
        watch:{
            //页面进出效果
            show(){
                var el = this.$el;
                var bds = this.$el.getElementsByClassName('bd');
                var that = this;
                this.status.switchFinish = false;
                if(this.show == true){
                    el.style.display = 'block';
                    Velocity(bds[0],{
                        width:'95%'
                    },{
                        duration:1000
                    })
                    Velocity(bds[1],{
                        height:'95%'
                    },{
                        duration:1000
                    })
                    Velocity(bds[2],{
                        height:'95%'
                    },{
                        duration:1000
                    })
                    Velocity(bds[3],{
                        width:'95%'
                    },{
                        duration:1000
                    })
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
                    Velocity(bds[0],{
                        width:'0'
                    },{
                        duration:1000
                    })
                    Velocity(bds[1],{
                        height:'0'
                    },{
                        duration:1000
                    })
                    Velocity(bds[2],{
                        height:'0'
                    },{
                        duration:1000
                    })
                    Velocity(bds[3],{
                        width:'0'
                    },{
                        duration:1000
                    })
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
        background-image:url(../assets/tooopen_sy_160139435598.jpg);
        background-position:50% 50%;
        background-repeat:no-repeat;
        background-color:#000;
        .hp-mask{
            background:rgba(0,0,0,.5);
            position:absolute;
            top:5px;
            left:5px;
            right:5px;
            bottom:5px;
            margin:auto;
            border-sizing:border-box;
            .bd{
                position:absolute;
                background:#aaa;
                box-shadow:-2px 2px 10px #fff;
            }
            .mask-bd-t{
                top:0;
                left:0;
                width:95%;
                height:1px;
            }
            .mask-bd-r{
                top:0;
                right:0;
                width:1px;
                height:95%;
            }
            .mask-bd-b{
                bottom:0;
                right:0;
                width:95%;
                height:1px;
            }
            .mask-bd-l{
                bottom:0;
                left:0;
                width:1px;
                height:95%;
            }
        }
    }
</style>