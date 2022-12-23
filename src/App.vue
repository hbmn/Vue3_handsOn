<script setup>
import Btn from "./components/Btn.vue";
import { ref } from "vue";

const items = ref([
  {
    id: 1,
    name: "アボカドバケット",
    description:
      "刻んだ野菜をアボカドと混ぜてディップに。こんがり焼いたバゲットとお召し上がりください。",
    price: 480,
    image: "/images/item1.jpg",
    soldOut: false,
    selected: false,
  },
  {
    id: 2,
    name: "あの日夢見たホットケーキ",
    description: "子供のころに食べたかった、あのホットケーキを再現しました。",
    price: 1100,
    image: "/images/item2.jpg",
    soldOut: false,
    selected: false,
  },
  {
    id: 3,
    name: "HOP WTR",
    description: "ロサンゼルス生まれのスパークリングウォーター。",
    price: 150,
    image: "/images/item3.jpg",
    soldOut: false,
    selected: false,
  },
  {
    id: 4,
    name: "チーズフレンチフライ",
    description:
      "イタリア産チーズをたっぷりかけたアツアツのフレンチフライ。みんな大好きな一品です。",
    price: 680,
    image: "/images/item4.jpg",
    soldOut: false,
    selected: false,
  },
]);
//金額を３桁でカンマつける
function pricePrefix(price) {
  return price.toLocaleString();
}

//現在の時刻取得
const timer = function () {
  const now = new Date();
  const hour = now.getHours();
  const min = now.getMinutes();
  const sec = now.getSeconds();
  return ` ${hour}時${min}分${sec}秒`;
};

//購入通知アラート
function alert() {
  window.alert(`${timer()}に購入しました`);
}

//商品在庫数でv-for表示
const itemLength = function () {
  if (items.length === 4) {
  }
  return true;
};
</script>

<template>
  <header class="header">
    <img src="/images/logo.svg" alt="" />
    <h1>ハンズオン</h1>
  </header>
  <Btn @click="alert()">購入する</Btn>
  <main class="main">
    <template v-for="item in items" :key="item.id">
      <div
        v-if="!item.soldOut"
        class="item"
        :class="{ 'selected-item': item.selected }"
        @click="item.selected = !item.selected"
      >
        <div class="thumbnail">
          <img :src="item.image" alt="" />
        </div>
        <div class="description">
          <h2>{{ item.name }}</h2>
          <p>{{ item.description }}</p>
          <span
            >¥<span class="price">{{ pricePrefix(item.price) }}</span></span
          >
        </div>
      </div>
    </template>
    <p v-if="itemLength()">商品はまだあります (true)</p>
    <p v-else="itemLength()">商品残りわずか(false)</p>
  </main>
</template>

<style scoped>
body {
  font-family: sans-serif;
  margin: 0;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#app {
  width: 90%;
  margin: 0 5%;
  color: #242424;
}

.header {
  display: flex;
  align-content: center;
  align-items: center;
  margin-top: 40px;
  margin-bottom: 40px;
}

.header > img {
  width: 100px;
  height: 100px;
  margin-right: 20px;
}

.header > h1 {
  font-size: 42px;
  font-weight: bold;
  line-height: 80px;
  margin-top: 0;
  margin-bottom: 0;
}

.main {
  display: grid;
  grid-template-columns: 3fr 3fr 3fr 3fr;
  column-gap: 24px;
  row-gap: 24px;
  margin-top: 20px;
}

.item {
  padding: 10px;
  cursor: pointer;
}

.item:hover {
  transition: 0.2s transform ease-out;
  transform: scale(1.05);
}

.item > div.thumbnail > img {
  width: 100%;
  height: calc(100%);
  object-fit: cover;
}

.item > div.description {
  text-align: left;
  margin-top: 20px;
}

.item > div.description > p {
  margin-top: 0px;
  margin-bottom: 0px;
  font-size: 18px;
  line-height: 25px;
}

.item > div.description > span {
  display: block;
  margin-top: 10px;
  font-size: 20px;
}

.item > div.description > span > .price {
  font-size: 28px;
  font-weight: bold;
}

.selected-item {
  background-color: #e3f2fd;
}
</style>
