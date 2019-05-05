<template>
    <div class="musicPlayPage">
      <img src="../../static/images/back.svg" id = "header_l" @click="back()">
      <div class="songname">{{this.$store.state.songName}}</div>
      <div class="singer">{{this.$store.state.singer}}</div>
      <img v-bind:src="'http://y.gtimg.cn/music/photo_new/T002R90x90M000'+this.$store.state.musicSrc+'.jpg?max_age=2592000'" class="palyerPic" v-bind:style="'transform: rotate('+this.t+'deg)'" ref="ampic">
      <ul class="process">
        <li class="time1">{{this.$store.state.time}}</li>
        <li class="process_contain" ref="proContain"  @click="runTo()">
          <div class="pro" ref="pro" v-bind:style="{width:this.$store.state.process}"></div>
        </li>
        <li class="time2">{{this.$store.state.nowtime}}</li>
      </ul>
      <div class="bottom">
        <img src="../../static/images/before.svg">
        <img src="../../static/images/playy.svg" v-show=this.$store.state.ifshow @click="musicplay()">
        <img src="../../static/images/pausee.svg" v-show=!this.$store.state.ifshow @click="musicplay()">
        <img src="../../static/images/after.svg">
      </div>
      <img src="../../static/images/sound.svg" class="sound">
    </div>
</template>

<script>
    export default {
      name: "musicPlayPage",
      data(){
        return{
          t:0
        }
      },
      methods:{
        back(){           //返回上一级
          window.history.go(-1);
          this.$store.commit('audioShow');
        },
        musicplay(){
          if(this.$store.state.ifshow===false){
            clearInterval(this.time)
            this.$store.commit('pause');
            this.$refs.audio.pause();
          }else {
            this.time = setInterval(()=> {
              this.t+=1;
            },100);
            this.$store.commit('play');
            this.$refs.audio.play();
          }
          this.$store.commit('timeRun');
        },
        runTo(){
          this.$store.commit('toPro',this.$refs.pro.offsetWidth/this.$refs.proContain.offsetWidth)
        }
      }
    }
</script>

<style scoped lang="stylus">
@import "../common/stylus/musicPlayPage.styl"
</style>
