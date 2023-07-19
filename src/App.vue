<template>
  <div class="body">
    <div class="top">
      <div class="left to-indigo-500 from-purple-500 bg-gradient-to-r font-bold">xGames
      </div>
      <div class="right">
        <button @click="onClick"> Switch Network </button>
      </div>
      <div class="zhong">
        Discover new xGames
      </div>
    </div>
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <div class="footer">
      <img src="./assets/github.png" alt="">
      <a href="https://github.com/LCL-sir/xgame">
        <p>· View Source Code</p>
      </a>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  methods: {
    onClick() {
      console.log(123)
    }
  }
}
</script>

<style scope>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}

.left {
  margin-left: 20px;
  text-align: start;
}

.font-bold {
  font-weight: 700;
  font-size: 1.25rem;
  line-height: 1.75rem;
  background-clip: text;
  color: #0000;
}

.to-indigo-500 {
  --tw-gradient-to: #6366f1;
}

.from-purple-500 {
  --tw-gradient-from: #a855f7;
  --tw-gradient-stops: var(--tw-gradient-from), var(--tw-gradient-to, #a855f700);
}

.bg-gradient-to-r {
  background-image: linear-gradient(to right, var(--tw-gradient-stops));
}

.right {
  margin-right: 20px;
  margin-top: -24px;
  text-align: end;
}

.right button {
  background-color: #733ce8;
  border: 0;
  width: 175px;
  height: 52px;
  padding: 12px 20px;
  border-radius: 10px;
  color: #cbd5e1;
  font-size: 19px;
  font-weight: 500;
  cursor: pointer;
}

.zhong {
  font-size: 28px;
  font-weight: 500;
  background: linear-gradient(to right, red, blue);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.footer {
  margin-top: 60px;

}

.footer img {
  width: 30px;
  line-height: 30px;
}

.footer img,
.footer p {
  display: inline-block;
  vertical-align: middle;
}

.footer p {
  color: #cbd5e1;
  font-size: 18px;
  margin-left: 5px;
}
</style>
