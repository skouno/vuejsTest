<template>
  <div id="app">
        <Home v-if="!isLogin"></Home> <!--条件付きレンダリング-->
        <Editor v-if="isLogin" :user="userData"></Editor>
  </div>
</template>

<script>
// 別のコンポーネントを相対パスでimportする。
import Home from "./components/Home.vue";
import Editor from "./components/Editor.vue";

export default {
  name: 'app',
  data() {
    return {
      isLogin: false, // ログイン状態を判別 → 条件付きレンダリング
      userData: null
    };
  },
  created: function() {
    firebase.auth().onAuthStateChanged(user => {
      console.log(user);
      if(user) {
        this.isLogin = true;
        this.userData = user;
      } else {
        this.isLogin = false;
        this.userData = null;
      };
    });
  },
  // template内で利用したいコンポーネントを {tag名: vueファイル}で定義する。
  // template内でHTMLタグのような形で定義したコンポーネントを読み出せる。
  components: {
    Home: Home,
    Editor: Editor
  }
};
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
