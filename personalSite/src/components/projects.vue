<template>
    <div id="pjs" class="page"
    :style="{'z-index':zIndex}"
    @mousemove="wave">
        <div class="pr-mask">
            <prCard 
            v-for="(item ,index) in projects" 
            :pr="item"
            :index="index"
            @open="open(index)"
            ></prCard>
            <prInfo 
            :show="infoShow"
            :data="showPageData"
            @closeIt="closeInfo"></prInfo>
        </div>
    </div>
</template>

<script>
import prCard from './pr/prCard'
import prInfo from './pr/prInfo'
    export default {
        components:{prCard, prInfo},
        props:['show'],
        data(){
            return {
                zIndex:80,
                infoShow:false,
                status:{
                    switchFinish:true
                },
                projects:[
                    {
                        name:'xxxx',
                        detail:'xxxx',
                        src:'....',
                        pic:'../assets/music.jpg',
                        isChoose:false,
                        info:'这是第一个项目'
                    },
                    {
                        name:'xxxx',
                        detail:'xxxx',
                        src:'....',
                        pic:'....',
                        isChoose:false,
                        info:'这是第二个项目'
                    },
                    {
                        name:'xxxx',
                        detail:'xxxx',
                        src:'....',
                        pic:'....',
                        isChoose:false,
                        info:'这是第三个项目'
                    },
                    {
                        name:'xxxx',
                        detail:'xxxx',
                        src:'....',
                        pic:'....',
                        isChoose:false,
                        info:'这是第四个项目'
                    }
                ],
                showPageData:null
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
            },
            open(index){
                this.infoShow = true;
                this.showPageData = this.projects[index]
            },
            closeInfo(){
                this.infoShow = false;
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
                        translateX:'120%'
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
    #pjs{
        display:none;
        background-image:url(../assets/5-120601093339.png);
        .pr-mask{
            width:90%;
            height:90%;
            border:3px solid #fff;
            position:absolute;
            top:0;
            left:0;
            right:0;
            bottom:0;
            margin:auto;
            background:rgba(0,0,0,.3);
            display:flex;
            align-content:space-around;
            align-items:center;
            justify-content:space-around;
            flex-wrap:wrap;
            overflow:auto;
        }
    }
</style>