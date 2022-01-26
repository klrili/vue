<template>
  <div class="container mt-5 mb-5">
    <div class="row align-items-center">
      <div class="col-8 text-white">
        <h6>
          {{ info }}
        </h6>
      </div>
      <div class="col-4 text-white text-uppercase text-end">
        <h5>MORE ABOUT OBLIX</h5>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    info: {
      type: String,
      required: false,
      default: '',
    },
  },
};
</script>
