<template>
  <div id="app"
  @mousewheel="scroll">
    <homePage :show="pages[0].show"></homePage>
    <personalInfo :show="pages[1].show"></personalInfo>
    <projects :show="pages[2].show"></projects>
    <PLZjob :show="pages[3].show"></PLZjob>
    <div class="dots-box">
      <span class="dot" 
      v-for="(page,index) in pages"
      @click="changePage(index)"
      >
        <span v-show="page.show"></span>
      </span>
      
    </div>
  </div>
</template>

<script>
//组件
import homePage from './components/homePage'
import personalInfo from './components/personalInfo'
import projects from './components/projects'
import PLZjob from './components/PLZjob'
export default {
  name: 'app',
  components : {homePage ,personalInfo ,projects ,PLZjob},
  data(){
    return {
      thisPage:0,
      canChange:true,
      timer:null,
      pages:[
        {
          index:0,
          show:true
        },
        {
          index:1,
          show:false
        },
        {
          index:2,
          show:false
        },
        {
          index:3,
          show:false
        }
      ]
    }
  },
  methods:{
    scroll(ev){
      if(!this.canChange)return;
      this.canChange = false;
      var that = this;
      this.timer = setTimeout(function(){
        that.canChange = true;
        clearTimeout(that.timer)
      },1000)
      if(ev.deltaY>0){
        this.thisPage ++;
        if(this.thisPage >= this.pages.length - 1)this.thisPage = this.pages.length - 1;
      }else{
        this.thisPage --;
        if(this.thisPage <= 0)this.thisPage = 0;
      }
      for(var i = 0;i<this.pages.length;i++){
        this.pages[i].show = false;
      }
      this.pages[this.thisPage].show = true;
    },
    changePage(index){
      if(!this.canChange)return;
      this.canChange = false;
      var that = this;
      this.timer = setTimeout(function(){
        that.canChange = true;
        clearTimeout(that.timer)
      },1000)
      for(var i = 0;i<this.pages.length;i++){
        this.pages[i].show = false;
      }
      this.pages[index].show = true;
    }
  }
}
</script>

<style lang="less">
html,body{
  width:100%;
  height:100%;
  margin:0;
  padding:0;
  background :#ddd;
  #app{
    width:100%;
    height:100%;
    position:relative;
    &>.page{
      width:95%;
      height:95%;
      margin:auto;
      position:absolute;
      top:0;
      left:0;
      right:0;
      bottom:0;
      border :1px solid #000;
      box-sizing:border-box;
    }
    .dots-box{
      width:30px;
      height:15%;
      z-index:1000;
      position:absolute;
      bottom :0;
      top:0;
      right:5%;
      margin: auto;
      display:flex;
      flex-direction:column;
      justify-content:space-around;
      align-content:center;
      align-items:center;
      .dot {
        width:15px;
        height:15px;
        border-radius:50%;
        background:rgba(0,0,0,.5);
        position:relative;
        span{
          display:block;
          width:60%;
          height:60%;
          border-radius:50%;
          background:rgba(255,255,255,.9);
          position:absolute;
          top:0;
          left:0;
          bottom:0;
          right:0;
          margin:auto;
        }
      }
    }
  }
}
</style>
