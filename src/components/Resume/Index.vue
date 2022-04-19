<template>
  <main>
    <p v-text="labelShow"></p>
    <h1 v-text="amountCurrency"></h1>
    <div class="graphic">
      <slot name="graphic"></slot>
    </div>
    <div class="action">
      <slot name="action"></slot>
    </div>
  </main>
</template>

<script>
const currenyFormatter = new Intl.NumberFormat("es-MX", {
  style: "currency",
  currency: "MXN",
});
export default {
  props: {
    label: {
      type: String,
    },
    date: {
      type: String,
      default: null,
    },
    amount: {
      type: Number,
      default: null,
    },
    totalAmount: {
      type: Number,
    },
  },
  computed: {
    amountShow() {
      return this.amount !== null ? this.amount : this.totalAmount;
    },
    labelShow() {
      return this.date == null ? this.label : this.date;
    },
    amountCurrency() {
      return currenyFormatter.format(this.amountShow);
    },
  },
  data() {
    return {};
  },
};
</script>

<style scoped>
main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100vh;
}

h1,
p {
  margin: 0;
  text-align: center;
}

h1 {
  margin-top: 14px;
  color: var(--brand-green);
}

.graphic {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  padding: 48px 24px;
  box-sizing: border-box;
}
</style>
