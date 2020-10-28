<template>
  <div class="slider d-flex" :style="{width:width?width:'100%',height:height?height:'450px'}">
    <div class="progress" :style="{display:simple&&'none'}" >
      <div class="progress-bar" :style="getProgress"></div>
    </div>
    <div 
      :key="id" 
      v-for="({img,id},ind) in slides" 
      :style="{transform:'translateX('+X+'%)'}"
      class="slide">
      <img :src="img" alt="-" :style="'transform:scaleY('+(ind==currentSlide?'1':'0.5')+')'">
    </div>
    <div class="left" @click="slide(1)">
      <b-icon icon="chevron-left" scale="2"></b-icon>
    </div>
    <div class="right" @click="slide(-1)">
      <b-icon icon="chevron-right" scale="2" ></b-icon>
    </div>
    <div class="icons" :style="{display:simple&&'none'}">
        <font-awesome-icon icon="check-circle" class="correct" @click="choose(true)" />
        <font-awesome-icon icon="times-circle" class="wrong" @click="choose(false)" />
      </div>
  </div>
</template>

<script>
export default {
  props:{
    width:String,
    height:String,
    slides:Array,
    simple:Boolean
  },
  data(){
    return {
      X:0,
      currentSlide:0,
      progress:0,
      choices:{},
      totalChoosen:0
    }
  },
  methods:{
    slide(by) {
      if(this.X == 0 && by > 0){
        return;
      }
      if(this.X == -100*(this.slides.length-1) && by < 0){
        return;
      }
      this.X = this.X + (by*100);
      if(by>0)
        this.currentSlide--;
      else
        this.currentSlide++;
    },
    choose(value){
      const id = this.slides[this.currentSlide].id
      if(!this.choices[id]){
        this.totalChoosen++;
      }
      this.choices[id] = {
        id,
        selected:value
      };
      this.slide(-1);
      if(this.totalChoosen===this.slides.length){
        this.$emit('finished',this.choices)
      } 
    }
  },
  computed:{
    getProgress(){
      return { width: (this.totalChoosen/this.slides.length * 100)+'%'}
    }
  }
}
</script>

<style scoped>
.slider{
  overflow: hidden;
  position: relative;
  padding:0 80px;
}
.progress{
  position: absolute;
  top:0;
  left:0;
  width:calc(100% - 174px);
  margin:0 87px;
  height:10px;
  z-index:100;
  background:rgba(0,0,0,0.1);
  border-radius: 0;
}
.progress-bar{
  background: rgba(73, 156, 189, 0.8);
  border-radius: 0;
}
.slide {
  min-width:100%;
  height:100%;
  padding:0 8px;
  display: flex;
  justify-content:center;
  align-items: center;
  transition: 0.4s ease-in-out;
}
.slide img {
  width:100%;
  object-fit: cover;
  transform:scaleY(0.5);
  transition: 0.4s ease-in-out;
}
.left,.right{
  position: absolute;
  z-index: 10;
  left:0;
  width:80px;
  height:100%;
  display: flex;
  justify-content: center;
  align-items: center;
  transition:all 0.1s ease;
}
.right{
  left:100%;
  transform: translateX(-100%);
}
.left:hover,.right:hover{
  background: rgba(0,0,0,0.2);
}
.icons{
  position: absolute;
  z-index:100;
  top:85%;
  left:50%;
  transform:translateX(-50%);
  font-size:2.5rem;
}
.correct,.wrong{
  margin:0 1rem;
}
.correct{
  color:rgb(145, 221, 145);
}
.wrong{
  color:rgb(197, 44, 44);
}
@media only screen and (max-width: 768px) {
  .slider{
    padding:0;
  }
  .progress{
    width:100%;
    margin:0;
  }
  .slide{
    padding:0;
  }
}
</style>