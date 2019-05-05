<template>
  <div id="app">
      <router-view></router-view>
      <music-play></music-play>
      <!--<audio src="http://ws.stream.qqmusic.qq.com/C400002on1X90kUdQm.m4a?fromtag=0&guid=126548448&vkey=C17DFA548FC475AB0FF71E709E2AC4733407390D721D1D3CFADB84C7072EE9DE93A6DBEE781CCE7D2792A20B247BBDD535E6635ABA395C00" autoplay controls></audio>-->
  </div>
</template>

<script>
  import musicPlay from './components/base/musicPlay'
export default {
  name: 'App',
  components:{
    musicPlay
  },
  created () {
    //在页面加载时读取sessionStorage里的状态信息
    if (sessionStorage.getItem("store")) {
      this.$store.replaceState(Object.assign({}, this.$store.state, JSON.parse(sessionStorage.getItem("store"))))
    }

    //在页面刷新时将vuex里的信息保存到sessionStorage里
    window.addEventListener("beforeunload", () => {
      sessionStorage.setItem("store", JSON.stringify(this.$store.state))
    })
  },
  mounted:function () {
    this.$store.commit('pageRefresh')
  }
}
</script>

<style>

</style>
