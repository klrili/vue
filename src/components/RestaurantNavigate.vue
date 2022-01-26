<template>
  <div class="id_navigate position-relative d-flex flex-column justify-content-end">
    <div
      class="id_bg_img"
      :style="{ backgroundImage: `url('${restaurantBackgroundImage}')` }"
    ></div>
    <div class="container id_navigate_container">
      <h4 class="id_menu_title text-white text-uppercase">choose menu</h4>
    </div>
    <div class="id_navigate_container bg-black bg-opacity-10">
      <div class="container">
        <div class="row row-cols-auto">
          <div @click="chooseRestaurant((state = 1))" class="col">
            <h1
              class="text-white id_choose_menu"
              :class="{
                'border-bottom border-3 border-white': state === 1,
              }"
            >
              West
            </h1>
          </div>
          <div @click="chooseRestaurant((state = 2))" class="col">
            <h1
              :class="{ 'border-bottom border-3 border-white': state === 2 }"
              class="text-white id_choose_menu"
            >
              East
            </h1>
          </div>
          <div @click="chooseRestaurant((state = 3))" class="col">
            <h1
              :class="{ 'border-bottom border-3 border-white': state === 3 }"
              class="text-white id_choose_menu"
            >
              Bar
            </h1>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    restaurantBackgroundImage: {
      type: String,
      required: false,
      default: '',
    },
  },
  data() {
    return {
      state: 1,
    };
  },
  methods: {
    chooseRestaurant() {
      this.$emit('change-restaurant', this.state);
    },
  },
};
</script>
