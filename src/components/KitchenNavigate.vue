<template>
  <div class="container">
    <div class="row justify-content-center mb-5">
      <div
        @click="ChooseMenu((menuId = idx))"
        v-for="(t, idx) of allKitchensObj"
        :key="idx"
        class="col-auto p-1"
      >
        <button
          class="text-white p-4 bg-transparent text-uppercase"
          :class="{ 'border-white': menuId === idx }"
          type="button"
        >
          {{ t }}
        </button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    allKitchensObj: {
      type: Object,
      required: false,
      default() {},
    },
  },
  data() {
    return {
      menuId: 0,
    };
  },
  methods: {
    ChooseMenu() {
      this.$emit('change-kitchen', this.menuId);
    },
  },
};
</script>
