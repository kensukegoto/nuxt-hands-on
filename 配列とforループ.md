# データから記事一覧を作成する

## ゴール

- layoutsディレクトリについて知る
- 画像の格納場所を知る
- 変数や配列を扱う
- Vueでforループを使う方法を知る

## 記事一覧を作成する

### まずはここから

```vue
<template>
  <section>
    <Title content="特集一覧" />
    <ul class="list">
      <li class="item">
        <a class="item__link" href="">
          <p class="item__title">記事タイトル</p>
          <time class="item__date">yyyy年mm月dd日</time>
        </a>
      </li>
      <li class="item">
        <a class="item__link" href="">
          <p class="item__title">記事タイトル</p>
          <time class="item__date">yyyy年mm月dd日</time>
        </a>
      </li>
      <li class="item">
        <a class="item__link" href="">
          <p class="item__title">記事タイトル</p>
          <time class="item__date">yyyy年mm月dd日</time>
        </a>
      </li>
      <li class="item">
        <a class="item__link" href="">
          <p class="item__title">記事タイトル</p>
          <time class="item__date">yyyy年mm月dd日</time>
        </a>
      </li>
    </ul>
  </section>
</template>

<style lang="scss" scoped>
.list{
  max-width: 960px;
  margin: 0 auto;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.item {

  width: calc(50% - 8px);
  margin-top: 1em;
  
  &__link{
    display: block;
    text-decoration: none;
  }

  &__title {
    font-weight: bold;
    color: #333;
  }
  &__date {
    color: #aaa;
  }
}
</style>
```

<img src="./image/3-1.png" width="480">

### リストスタイルなどCSSをリセットする

`layouts/default.vue`を下記と置き換える

```vue
<template>
  <div>
    <Nuxt />
  </div>
</template>

<style>
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
ul{
  list-style-type: none;
}
img{
  max-width: 100%;
}
</style>
```

## 一覧にサムネを追加する

### 画像の置き場所

画像はstaticディレクトリ、またはassetsディレクトリに置くルール<br>
<br>
webpackで画像容量を小さくするなど処理を入れたい場合はassets（別途設定必要）<br>
特に何もしないならばstatic

### staticに画像を置く

画像のzipフォルダをDLし解凍<br>
<br>
staticに解凍したimageフォルダを配置する

### 画像を表示する

pages/index.vueを下記と置き換える<br>
差分は\<figure\>の追加部分

```vue
<template>
  <section>
    <Title content="特集一覧" />
    <ul class="list">
      <li class="item">
        <a class="item__link" href="">
          <figure class="item__img"><img src="image/20200904/img_01.jpg" alt=""></figure>
          <p class="item__title">記事タイトル</p>
          <time class="item__date">yyyy年mm月dd日</time>
        </a>
      </li>
      <li class="item">
        <a class="item__link" href="">
          <figure class="item__img"><img src="image/20200904/img_01.jpg" alt=""></figure>
          <p class="item__title">記事タイトル</p>
          <time class="item__date">yyyy年mm月dd日</time>
        </a>
      </li>
      <li class="item">
        <a class="item__link" href="">
          <figure class="item__img"><img src="image/20200904/img_01.jpg" alt=""></figure>
          <p class="item__title">記事タイトル</p>
          <time class="item__date">yyyy年mm月dd日</time>
        </a>
      </li>
      <li class="item">
        <a class="item__link" href="">
          <figure class="item__img"><img src="image/20200904/img_01.jpg" alt=""></figure>
          <p class="item__title">記事タイトル</p>
          <time class="item__date">yyyy年mm月dd日</time>
        </a>
      </li>
    </ul>
  </section>
</template>

<style lang="scss" scoped>
.list{
  max-width: 960px;
  margin: 0 auto;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.item {

  width: calc(50% - 8px);
  margin-top: 1em;
  
  &__link{
    display: block;
    text-decoration: none;
  }

  &__title {
    font-weight: bold;
    color: #333;
  }
  &__date {
    color: #aaa;
  }
}
</style>
```

<img src="./image/3-2.png" width="480">

## 各liをコンポーネントにする

### Linkコンポーネントを作成する

components配下に`Link.vue`ファイルを作成し下記をコピペ<br>
liの中身を移動

```vue
<template>
  <li class="item">
    <a class="item__link" href="">
      <figure class="item__img"><img src="image/20200904/img_01.jpg" alt=""></figure>
      <p class="item__title">記事タイトル</p>
      <time class="item__date">yyyy年mm月dd日</time>
    </a>
  </li>
</template>

<style lang="scss" scoped>
.item {
  
  &__link{
    display: block;
    text-decoration: none;
  }

  &__title {
    font-weight: bold;
    color: #333;
  }
  &__date {
    color: #aaa;
  }
}
</style>
```

### Linkコンポーネントを表示

pages/index.vueの\<template\>タグを下記で置き換える

```vue
<template>
  <section>
    <Title content="特集一覧" />
    <ul class="list">
      <Link />
      <Link />
      <Link />
      <Link />
    </ul>
  </section>
</template>
```

## 配列を元にLinkを作成する

### 変数や配列の扱い方

実装してから確認をして行くスタイル<br>
pages/index.vueの\<template\>を下記と置き換える<br>

```vue
<template>
  <section>
    <Title content="特集一覧" />
    <ul class="list">
      <Link />
      <Link />
      <Link />
      <Link />
    </ul>
    <pre>
      {{ hensu }}
      {{ hairetu }}
    </pre>
    <p>私は{{ name }}です。</p>
  </section>
</template>
```

\<template\>の後ろに下記を追加

```vue
<script>
export default {
  data: () => {
    return {
      hensu: "変数",
      hairetu: [1,2,3,4,5],
      name: "kensuke goto"
    }
  }
}
</script>
```

\<template\>で使えるJSの変数として登録する必要がある<br>
dataメソッドの返り値のオブジェクトにキーバリュー型で登録が出来る

### 記事配列を作る

pages/index.vueの\<template\>と\<script\>をそれぞれ下記に置き換える

・template

```vue
<template>
  <section>
    <Title content="特集一覧" />
    <ul class="list">
      <Link />
      <Link />
      <Link />
      <Link />
    </ul>
    <pre>
      {{ list }}
    </pre>
  </section>
</template>
```

・script

```vue
<script>
export default {
  data: () => {
    return {
      list: [
        { "title": "タイトル１", "date": "2020年9月4日", "img": "image/20200904/img_01.jpg", "link": "20200904"},
        { "title": "タイトル２", "date": "2020年9月5日", "img": "image/20200905/img_01.jpg", "link": "20200905"},
        { "title": "タイトル３", "date": "2020年9月6日", "img": "image/20200906/img_01.jpg", "link": "20200906"},
        { "title": "タイトル４", "date": "2020年9月7日", "img": "image/20200907/img_01.jpg", "link": "20200907"}
      ]
    }
  }
}
</script>
```

### 配列をforループする

listの要素数だけlinkが表示される<br>
データの反映はこの後でしていく

```vue
<template>
  <section>
    <Title content="特集一覧" />
    <ul class="list">
      <Link
        class="item" 
        v-for="(item,index) of list"
        :key="index"
      />
    </ul>
  </section>
</template>
```

`:key="index"`はLinkのkey属性に変数indexを設定するという意味<br>
属性を設定する場合、文字列や数字か、変数かで書き方が変わる。<br>
文字列や変数の場合は、「:」は不要

## Linkに配列の内容を反映する

### Linkに配列の内容を渡す

Linkタグを下記と置き換え

```vue
<Link
  class="item" 
  v-for="(item,index) of list"
  :key="index"
  :title="item.title"
  :date="item.date"
  :img="item.img"
  :link="item.link"
/>
```

### Linkで渡された内容を反映する

components/Link.vueを下記と置き換える<br>
propsを設定して渡って来たデータを扱えるようにする

```vue
<template>
  <li class="item">
    <a class="item__link" :href="link">
      <figure class="item__img"><img :src="img" alt=""></figure>
      <p class="item__title">{{ title }}</p>
      <time class="item__date">{{ date }}</time>
    </a>
  </li>
</template>
<script>
export default {
  props : ["title","date","img","link"]
}
</script>
<style lang="scss" scoped>
.item {
  
  &__link{
    display: block;
    text-decoration: none;
  }

  &__title {
    font-weight: bold;
    color: #333;
  }

  &__date {
    color: #aaa;
  }
}
</style>
```

<img src="./image/3-3.png" width="480">

リンクをクリックするとエラーっぽい表示がされる<br>
リンク先は後で作成する

## 完成

盛りだくさんでしたが下記項目の実装方法をマスターしました

- layoutsディレクトリについて知る
- 画像の格納場所を知る
- 変数や配列を扱う
- Vueでforループを使う方法を知る
