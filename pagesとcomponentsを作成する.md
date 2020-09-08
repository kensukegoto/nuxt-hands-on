# pagesとcomponentsを作成する

## ゴール

コンポーネントとは何か？を理解する。スタイルをどのように設定するかを習得する。Vueファイル間でデータを渡す方法を知る。

## pagesとは？

このディレクトリ内の.vueファイルが遷移出来るページとなる

### 開発モードでNuxtアプリを立ち上げよう

下記コマンドを実行し、ブラウザでNuxtアプリを表示する

```
yarn dev
```

### ページを作ってみよう

pages/index.vueを複製し、pages/index2.vueと命名する<br>
http://localhost:3000/index2 へアクセスすると<br>
urlを持ったページが作られた事を確認出来る

## componentsとは？

pageを構成するパーツ。Vueのページは、複数のcomponentを組み合わせで構成される。components配下の.vueファイルがcomponentとして扱われる。各pageで使い回す事が出来る。

## 初めての独自コンポーネントを作成する

components配下に`Title.vue`ファイルを作成し下記をコピペ<br>
中の文字を入れ替えて汎用的に使えるh2のタイトルを想定

```vue
<template>
  <h2>H2タイトル</h2>
</template>
```

`pages/index.vue`ファイルを下記に変更

```vue
<template>
  <div>
    <Title />
  </div>
</template>
```

下記のようにブラウザで表示されれば成功！

<img src="./image/2-1.png" width="300">

## スタイルを調整する

Title.vueを開き中身を下記と置き換える<br>
Vueで作成するページはVueコンポーネントの組み合わせで構成される<br>
スタイルは各コンポーネント毎に設定する

```vue
<template>
  <h2>H2タイトル</h2>
</template>

<style scoped>
h2 {
  font-size: 18px;
  font-weight: bold;
  text-align: center;
}
</style>
```

## scopedとは？

styleタグに`scoped`を付けると、そこで記述されるスタイルは、そのVueファイル内でのみ適用される

## Sassを使えるようにしよう

デフォルトでは使えない<br>
下記モジュールをインストール

```
yarn add node-sass sass-loader
```

Title.vueを下記に置き換える

```vue
<template>
  <h2>H2タイトル</h2>
</template>

<style lang="scss" scoped>
h2{
  font-size: 18px;
  font-weight: bold;
  text-align: center;
  margin-bottom: 1em;
  position: relative;
  &::before{
    content: '';
    position: absolute;
    bottom: -15px;
    display: inline-block;
    width: 60px;
    height: 5px;
    left: 50%;
    transform: translateX(-50%);
    background-color: black;
    border-radius: 2px;
  }
}
</style>
```

Sassが有効になった事を確認

<img src="./image/2-2.png" width="300">


## Vueファイル間でデータの受け渡しをする

ページのVueファイルからコンポーネントのVueファイルを読むというようにVueファイルは入れ子にする事が出来る<br>
入れ子になったVueファイル間でデータを受け渡したい場合がある<br>
<br>
※Vueを初めて触る人にとって理解しにくい部分かもしれません<br>
触っているうちに要領を得て来る部分だろう、とフワッと理解してもらえれば輪郭がハッキリして来ると思います<br>

### 手順

```
1.親のVueファイルで、コンポーネントの属性としてデータを追加する
2.設定された属性を子のVueファイルで読めるようにする
```

### 1.親のVueファイルで、コンポーネントの属性としてデータを追加する

```vue
<template>
  <div>
    <Title content="特集一覧" />
  </div>
</template>
```

### 2.設定された属性を子のVueファイルで読めるようにする

ポイントは２つ<br>
親からデータを受け取るために`props`を指定する<br>
受け取って変数に格納されたデータをマスタッシュで括りページに表示させる

```vue
<template>
  <h2>{{ content }}</h2>
</template>

<script>
export default {
  props: ["content"]
}
</script>

<style lang="scss" scoped>
h2{
  font-size: 18px;
  font-weight: bold;
  text-align: center;
  margin-bottom: 1em;
  position: relative;
  &::before{
    content: '';
    position: absolute;
    bottom: -15px;
    display: inline-block;
    width: 60px;
    height: 5px;
    left: 50%;
    transform: translateX(-50%);
    background-color: black;
    border-radius: 2px;
  }
}
</style>
```

## 完成

ページのパーツとしてコンポーネントを作成する事とコンポーネントへのスタイルをどのように付けて行くかを習得出来ました。あとは、このコンポーネントを増やして行く事でサイトを作成する事が出来ます。