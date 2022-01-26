<template>
  <div class="container bg-white">
    <h2 v-if="title.length > 0" class="text-center p-4 text-uppercase">{{ title }}</h2>
    <div class="border-top p-1 m-2"></div>
    <div class="id_menu_block p-3">
      <div v-for="menuNameId of menuObj" :key="menuNameId" class="id_block">
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
  <div>{{ title }}</div>
</template>
<script>
export default {
  props: {
    title: {
      type: String,
      required: false,
      default: '',
    },
    menuObj: {
      type: Object,
      required: false,
      default() {},
    },
  },
};
</script>
