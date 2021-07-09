<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <news v-if="isRouterAlive"></news>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import News from './components/news.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld
    News
  },
  created() {
    /* 第一次运行是启用，添加news的初始数据
    let data = {
      content: "this is new1",
      comments: [],
      commentsNumber: 0
    };
    localStorage.setItem('news1',JSON.stringify(data));
    */
  //  let data = {
  //     content: "this is new1",
  //     comments: [],
  //     commentsNumber: 0
  //   };
  //   localStorage.setItem('news1',JSON.stringify(data));

  },
  provide() {
    return {
      reload: this.reload
    }
  },
  data() {
    return {
      isRouterAlive: true
    }
  },
  methods: {
    reload() {
      this.isRouterAlive = false;
      this.$nextTick(function () {
        this.isRouterAlive = true;
      })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
