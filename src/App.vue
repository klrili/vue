<template>
  <div class="wrapper">
    <RestaurantNavigate @change-restaurant="chooseRestaurant" :restaurantBackgroundImage="imgUrl" />
    <RestaurantInfo :info="restaurantInfo" />
    <KitchenNavigate @change-kitchen="chooseMenu" :allKitchensObj="allKitchens" />
    <MenuCard :title="changedTitle" :menuObj="menuObj" />

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
import RestaurantNavigate from './components/RestaurantNavigate.vue';
import RestaurantInfo from './components/RestaurantInfo.vue';
import KitchenNavigate from './components/KitchenNavigate.vue';
import MenuCard from './components/MenuCard.vue';
export default {
  name: 'App',
  components: {
    RestaurantNavigate,
    RestaurantInfo,
    KitchenNavigate,
    MenuCard,
  },
  data() {
    return {
      stock: [],
      kitchens: [],
      menu: [],
      menuTitle: '',
    };
  },
  methods: {
    chooseRestaurant(state) {
      if (state === 1) {
        (this.kitchens = this.stock.west),
          (this.menu = this.stock.west.menuName[0]),
          (this.menuTitle = this.stock.west.kitchen[0]);
      } else {
        if (state === 2) {
          (this.kitchens = this.stock.east),
            (this.menu = this.stock.east.menuName[0]),
            (this.menuTitle = this.stock.east.kitchen[0]);
        } else {
          if (state === 3) {
            (this.kitchens = this.stock.bar),
              (this.menu = this.stock.bar.menuName[0]),
              (this.menuTitle = this.stock.bar.kitchen[0]);
          }
        }
      }
    },
    chooseMenu(menuId) {
      this.menu = this.kitchens.menuName[menuId];
      this.menuTitle = this.kitchens.kitchen[menuId];
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
  computed: {
    imgUrl() {
      return this.kitchens.image;
    },
    restaurantInfo() {
      return this.kitchens.restaurantDescription;
    },
    allKitchens() {
      return this.kitchens.kitchen;
    },
    changedTitle() {
      return this.menuTitle;
    },
    menuObj() {
      return this.menu;
    },
  },
};
</script>

<style src="./css/styles.css"></style>
<style src="./css/bootstrap.min.css"></style>
