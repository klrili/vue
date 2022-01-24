<template>
  <div class="wrapper">
    <div class="id_navigate position-relative d-flex flex-column justify-content-end">
      <div class="id_bg_img" :style="{ backgroundImage: `url('${kitchens.image}')` }"></div>
      <div class="container id_navigate_container">
        <h4 class="id_menu_title text-white text-uppercase">choose menu</h4>
      </div>
      <div class="id_navigate_container bg-black bg-opacity-10">
        <div class="container">
          <div class="row row-cols-auto">
            <div @click="ChooseRestaurant((id = 1))" class="col">
              <h1
                class="text-white id_choose_menu"
                :class="{ 'border-bottom border-3 border-white': id === 1 }"
              >
                West
              </h1>
            </div>
            <div @click="ChooseRestaurant((id = 2))" class="col">
              <h1
                :class="{ 'border-bottom border-3 border-white': id === 2 }"
                class="text-white id_choose_menu"
              >
                East
              </h1>
            </div>
            <div @click="ChooseRestaurant((id = 3))" class="col">
              <h1
                :class="{ 'border-bottom border-3 border-white': id === 3 }"
                class="text-white id_choose_menu"
              >
                Bar
              </h1>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="container mt-5 mb-5">
      <div class="row align-items-center">
        <div class="col-8 text-white">
          <h6>
            {{ kitchens.restaurantDescription }}
          </h6>
        </div>
        <div class="col-4 text-white text-uppercase text-end">
          <h5>MORE ABOUT OBLIX</h5>
        </div>
      </div>
    </div>

    <div class="container">
      <div class="row justify-content-center mb-5">
        <div
          @click="ChooseMenu(idx)"
          v-for="(t, idx) of kitchens.kitchen"
          :key="idx"
          class="col-auto p-1"
        >
          <button class="text-white p-4 bg-transparent text-uppercase" type="button">
            {{ t }}
          </button>
        </div>
      </div>
    </div>
    <div class="container bg-white">
      <h2 v-if="menuTitle.length > 0" class="text-center p-4 text-uppercase">{{ menuTitle }}</h2>
      <div class="border-top p-1 m-2"></div>
      <div class="id_menu_block p-3">
        <div v-for="menuNameId of menu" :key="menuNameId" class="id_block">
          <div v-if="menuNameId.menuTitle" class="border-bottom border-3 border-dark"></div>
          <h3 v-if="menuNameId.menuTitle" class="fw-bold text-uppercase m-3">
            {{ menuNameId.menuTitle }}
          </h3>
          <div v-if="!menuNameId.menuTitle" class="d-flex justify-content-between">
            <h5>{{ menuNameId.menuCol }}</h5>
            <h5>{{ menuNameId.menuNum }}</h5>
          </div>
        </div>
      </div>
    </div>

    <div class="id_menu_end position-relative">
      <div
        class="id_bg_rest"
        :style="{ 'background-image': `url(${require('./img/restaurant.jpg')})` }"
      ></div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'App',
  data() {
    return {
      stock: [],
      kitchens: [],
      menu: [],
      menuTitle: [],
    };
  },
  methods: {
    ChooseRestaurant(id) {
      id === 1
        ? ((this.kitchens = this.stock.west),
          (this.menu = this.stock.west.menuName[0]),
          (this.menuTitle = this.stock.west.kitchen[0]))
        : id === 2
        ? ((this.kitchens = this.stock.east),
          (this.menu = this.stock.east.menuName[0]),
          (this.menuTitle = this.stock.east.kitchen[0]))
        : id === 3
        ? ((this.kitchens = this.stock.bar),
          (this.menu = this.stock.bar.menuName[0]),
          (this.menuTitle = this.stock.bar.kitchen[0]))
        : null;
    },
    ChooseMenu(idx) {
      this.menu = this.kitchens.menuName[idx];
      this.menuTitle = this.kitchens.kitchen[idx];
    },
  },
  mounted() {
    axios
      .get('https://mocki.io/v1/c9adda75-a084-4945-87f5-b9560582c6a0')
      .then(
        (res) => (
          (this.stock = res.data),
          (this.kitchens = res.data.west),
          (this.menu = res.data.west.menuName[0]),
          (this.menuTitle = res.data.west.kitchen[0])
        ),
      );
  },
};
</script>

<style src="./css/styles.css"></style>
<style src="./css/bootstrap.min.css"></style>
