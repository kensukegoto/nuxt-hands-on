# ajaxを扱う

外部からjsonなどでデータを取得して扱いたい

## ゴール

外部データを扱える

## ajaxを扱うツールをインストール

### インストール

```
yarn add @nuxtjs/axios
```

### nuxtモジュールとは？

nuxtが公式で配布している追加拡張機能<br>
ajaxを扱うライブラリであるaxiosを拡張したモジュールがnuxt公式である<br>
通常のaxiosもnuxt内で使えるが、更に機能拡張されたnuxtモジュール版をここでは使う<br>
ただ、このハンズオンでは、その拡張機能には触れない…

### 有効にする

nuxtモジュールを使うにはインストール後に設定ファイルで有効にする必要がある<br>
nuxt.config.jsを開きmodulesの項目を探し下記と置き換え

```js
  /*
  ** Nuxt.js modules
  */
  modules: [
    '@nuxtjs/axios',
  ],
```

### axiosを使う

pages/index.vueの\<script\>を下記と置き換える

```vue
<script>
export default {
  asyncData(context) {
    return context.app.$axios.$get("http://nuxt-hands-on.s3-website.ap-northeast-2.amazonaws.com/api/list.json")
      .then(res => {
        console.log(res)
        return {
          list: res
        }
      })
  }
}
</script>
```

非同期データをNuxtに埋め込みたい場合は、asyncDataメソッドを使う<br>
非同期処理完了後にコンポーネントが作成される<br>
つまり、コンポーネントで非同期データを使用出来る<br>
<br>
$getがPromiseベース。コールバック関数の返り値をキーバリュー型のオブジェクトとして登録するとdataメソッド同様に、\<template\>内で変数として扱えるようになる

## 完成

ajaxで取得しデータをページに埋め込む事が出来るようになりました！