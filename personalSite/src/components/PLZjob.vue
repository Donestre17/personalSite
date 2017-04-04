<template>
    <div id="job" class="page"
    :style="{'z-index':zIndex}"
    @mousemove="wave"></div>
</template>

<script>
    export default {
        props:['show'],
        data(){
            return {
                zIndex:70,
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
                        translateY:'120%'
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
    #job{
        display:none;
        background:#666
    }
</style>