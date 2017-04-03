<template>
    <div id="hp" class="page"
    v-show="show"
    :style="{'z-index':zIndex}">
        <h1>这是首页</h1>
    </div>
</template>

<script>
    export default {
        props:['show'],
        data(){
            return {
                zIndex:100,
                starty:null,
                disy:null,
                status:{
                    isStart:false
                }
            }
        },
        
    }
</script>

<style lang="less" scoped>
    #hp{
        background:#3399CC;
    }
</style>