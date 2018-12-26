<template>
  <div class="editor">
    <h1>エディター画面</h1>
    <span>{{ user.displayName }}</span>
    <button @click="logout">ログアウト</button>
    <div class="editorWrapper">
      <!-- v-model: inputやtextareaの状態をコンポーネントのデータへ格納する(データバインディング)。 -->
      <textarea class="markdown" v-model="markdown"></textarea>
      <!-- v-html: 指定した値を直接HTMLとして描画する。 -->
      <div class="preview" v-html="preview()"></div>
    </div>
  </div>
</template>
<script>
import marked from "marked";
export default {
    name: "editor",
    props: ["user"],
    data() {
        return {
          markdown: "" // マークダウンで記述されたテキスト。
        };
    },
    methods: {
      logout: function() {
        firebase.auth().signOut();
      },
      preview: function() {
        return marked(this.markdown);  // markedを利用して、markdown → HTMLで返す。
      }
    }
};
</script>
<style lang="scss" scoped>
// scoped: 記述したコンポーネント内でしか適用されない
// (自動的にhtmlに個別の属性を割り当て、その属性のみにCSSが適用されるように変換してくれる)。
.editorWrapper {
  display: flex;
}
.markdown {
  width: 50%;
  text-align: left;
}
</style>
