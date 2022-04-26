<template>
  <div>
    <svg
      @touchstart="tap"
      @touchmove="tap"
      @touchend="untap"
      viewBox="0,0 300 200"
    >
      <line
        stroke="#c4c4c4"
        stroke-width="2"
        x1="0"
        :y1="zero"
        x2="300"
        :y2="zero"
      />
      <polyline
        fill="none"
        stroke="#0689B0"
        stroke-width="2"
        :points="points"
      />
      <line
        v-show="showPointer"
        stroke="#04b500"
        stroke-width="2"
        :x1="pointer"
        y1="0"
        :x2="pointer"
        y2="200"
      />
    </svg>
    <p>Últimos 30 días</p>
  </div>
</template>

<script>
export default {
  props: {
    amounts: {
      type: Array,
      default: () => [],
    },
  },
  computed: {
    points() {
      const total = this.amounts.length;
      return this.amounts.reduce((points, amount, index) => {
        const x = (300 / total) * (index + 1);
        const y = this.amountToPixels(amount);
        return `${points} ${x},${y}`;
      }, "0,100");
    },
    zero() {
      return this.amountToPixels(0);
    },
  },
  data() {
    return {
      showPointer: false,
      pointer: 0,
    };
  },

  methods: {
    //Calcula la grafica
    amountToPixels(amount) {
      const min = Math.min(...this.amounts);
      const max = Math.max(...this.amounts);

      const amountAbs = amount + Math.abs(min);
      const minmax = Math.abs(max) + Math.abs(min);

      return 200 - ((amountAbs * 100) / minmax) * 2;
    },

    //target y touches son de javascript y no vue js.
    tap({ target, touches }) {
      this.showPointer = true;
      const elementWidth = target.getBoundingClientRect().width;
      const elementX = target.getBoundingClientRect().x;
      const touchX = touches[0].clientX;

      this.pointer = ((touchX - elementX) * 300) / elementWidth;

      //Falta enviar el emit
    },

    untap() {
      this.showPointer = false;
    },
  },
};
</script>

<style scoped>
svg {
  width: 100%;
}

p {
  text-align: center;
}
</style>
