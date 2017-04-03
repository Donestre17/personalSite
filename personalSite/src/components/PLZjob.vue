<template>
    <div id="job" class="page"
    v-show="show"
    :style="{'z-index':zIndex}"></div>
</template>

<script>
    export default {
        props:['show'],
        data(){
            return {
                zIndex:70
            }
        }
    }
</script>

<style lang="less" scoped>
    #job{
        background:#666
    }
</style>