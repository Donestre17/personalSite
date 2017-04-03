<template>
    <div id="pjs" class="page"
    v-show="show"
    :style="{'z-index':zIndex}"></div>
</template>

<script>
    export default {
        props:['show'],
        data(){
            return {
                zIndex:80
            }
        }
    }
</script>

<style lang="less" scoped>
    #pjs{
        background:#a93434
    }
</style>