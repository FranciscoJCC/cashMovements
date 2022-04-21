<template>
  <div class="movement">
    <div class="content">
      <h4 v-text="title"></h4>
      <p v-text="description"></p>
    </div>
    <div class="action">
      <img src="@/assets/trash.svg" alt="Borrar" @click="removeItem(id)" />
      <p
        :class="[{ red: isNegative, green: !isNegative }]"
        v-text="amountCurrency"
      ></p>
    </div>
  </div>
</template>

<script>
const currenyFormatter = new Intl.NumberFormat("es-MX", {
  style: "currency",
  currency: "MXN",
});
export default {
  props: {
    id: {
      type: Number,
      default: 0,
    },
    title: {
      type: String,
      default: "",
    },
    description: {
      type: String,
      default: "",
    },
    amount: {
      type: Number,
      default: 0,
    },
  },
  computed: {
    amountCurrency() {
      return currenyFormatter.format(this.amount);
    },
    isNegative() {
      return this.amount < 0;
    },
  },
  data() {
    return {
      data() {
        return {};
      },
    };
  },
  methods: {
    removeItem(id) {
      this.$emit("remove", id);
    },
  },
};
</script>

<style scoped>
.movement {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 16px;
  background-color: #e6f9ff;
  border-radius: 8px;
  box-sizing: border-box;
}

.movement .content {
  width: 100%;
}

.movement .action {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-direction: column;
}

h4,
p {
  margin: 0;
  padding: 0;
}

h4 {
  margin-bottom: 8px;
}

.movement .action img {
  margin-bottom: 16px;
}

.red {
  color: red;
}

.green {
  color: green;
}
</style>
