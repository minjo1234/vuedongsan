<template>
    <img alt="Vue logo" src="./assets/logo.png" />

    <transition name="fade">
    <Modal @modal_close="model_state=false" :onerooms="onerooms" :click_Number="click_Number" :model_state="model_state" />
    </transition>

    <div class="menu">
      <a href="" v-for="(a, i) in home" :key="i"> {{ a }}</a>
    </div>

    <Discount v-show="showDiscount" v-bind="object" :name="object.name" :age="object.age"/>

    <Card @open_modal="model_state = true; click_Number = $event" :oneroom="onerooms[i]" v-for="(a,i) in onerooms" :key="a"/>

    <button @click="priceSortAsc">가격 오름차순 정렬</button>
    <button @click="priceSortDesc">가격 내림차순 정렬</button>
    <button @click="koreanSortAsc">가나다순 정렬</button>
    <button @click="sortBack">되돌리기</button>
</template>

<script>
import Discount from "./Discount.vue";
import data from "./data";
import Modal from "./Modal.vue";
import Card from "./Card.vue";

export default {
  name: "App",
  data() {
    return {
      showDiscount : true,
      object : { name : 'kim' , age : 20},
      // 데이터 보관함 , object(key, value) 형식으로 저장
      // 1.데이터바인딩의 이유 하드코딩할경우 나중에 변경이 어렵다.
      // 2.Vue의 실시간 자동 렌더링을 사용하기 위해서이다. -> data와 관련있는 HTML에도 실시간으로 반영된다.
      priceArray: [60, 100, 150],
      products: ["역상동원룸", "천호동원룸", "마포구원룸"],
      home: ["Home", "Shop", "About"],
      declaration: [0, 0, 0],
      model_state: false,
      images: [
        require("./assets/room0.jpg"),
        require("./assets/room1.jpg"),
        require("./assets/room2.jpg"),
      ],
      onerooms: data,
      onerooms_org : [...data],
      click_Number: 0,
    };
  },

  methods: {
    model_open_and_close() {
      this.model_state = !this.model_state;
      return this.model_state;
    },
    priceSortAsc() {
      this.onerooms.sort(function (a,b){
        return a.price -b.price
      })
    },
    sortBack() {
      this.onerooms = [...this.onerooms_org];
    },
    priceSortDesc() {
      this.onerooms.sort(function (a,b){
        return b.price - a.price
      })
    },
    koreanSortAsc() {
      this.onerooms.sort(function (a,b) {
        if (a.title > b.title) return 1;
        if (a.title < b.title) return -1;
        return 0;
      })
    },
  },

  mounted() {
    setTimeout( ()=>{

    }, 2000);
  },

  components: {
    Discount: Discount,
    Modal: Modal,
    Card : Card,
  },
};
</script>


<style>

.fade-enter-from , .fade-leave-to{
  opacity: 0;
}

 .fade-enter-active , .fade-leave-active {
  transition: all 1s;

}
.fade-enter-to , .fade-leave-from {
  opacity: 1;
}

.start{
  opacity: 0;
  transition: all 1s;
}

.end{
  opacity: 1;
}

body {
  margin: 0;
}

div {
  box-sizing: border-box;
}

.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}

.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}

.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding: 10px;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}
</style>
