<template>
    <div id="info" class="page"
    v-show="show"
    :style="{'z-index':zIndex}"></div>
</template>

<script>
    export default {
        props:['show'],
        data(){
            return {
                zIndex:90
            }
        }
    }
</script>

<style lang="less" scoped>
    #info{
        background:greenyellow
    }
</style>