<template>
  <news v-if="isRouterAlive"></news>
</template>

<script>
import News from './components/news.vue'

export default {
  name: 'App',
  components: {
    News
  },
  created() {
    /* 第一次运行时启用，添加news的初始数据
    let data = {
      content: "this is new1",
      comments: [],
      commentsNumber: 0
    };
    localStorage.setItem('news1',JSON.stringify(data));
    */
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
