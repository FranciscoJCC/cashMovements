<template>
  <div class="movement">
    {{ title }}
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: "",
    },
  },
  data() {
    return {};
  },
};
</script>

<style></style>
