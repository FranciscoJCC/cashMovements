<template>
  <header>
    <img src="@/assets/cashflow.svg" alt="logo" @click="reload" />
    <h1><span>Cash</span>Flow</h1>
    <span></span>
  </header>
</template>

<script>
export default {
  data() {
    return {};
  },

  methods: {
    reload() {
      location.reload();
    },
  },
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 100vh;
}

img,
span {
  width: 48px;
}

h1 {
  font-size: 1.4rem;
  color: var(--bran-blue);
}

h1 span {
  color: var(--brand-green);
}
</style>
