<template>
  <button @click="showModal = true">Agregar movimiento</button>

  <teleport to="#app">
    <Modal v-show="showModal" @closeModal="showModal = !showModal">
      <form>
        <div class="field">
          <label for="">Titulo</label>
          <input type="text" v-model="movement.title" />
        </div>
        <div class="field">
          <label for="">Cantidad</label>
          <input type="number" v-model="movement.amount" />
        </div>
        <div class="field">
          <label for="">Descripción</label>
          <textarea rows="4" v-model="movement.description"></textarea>
        </div>
        <div class="field">
          <label for="">Tipo de movimiento</label>
          <label for="" class="radio-label">
            <input type="radio" v-model="type" value="ingreso" />
            <span>Ingreso</span>
          </label>
          <label for="" class="radio-label">
            <input type="radio" v-model="type" value="gasto" />
            <span>Gasto</span>
          </label>
        </div>
        <div class="action">
          <button type="button" @click="saveMovement(movement)">
            Agregar movimiento
          </button>
        </div>
      </form>
    </Modal>
  </teleport>
</template>

<script>
import Modal from "./Modal.vue";
export default {
  emits: ["saveMovement"],
  components: { Modal },
  data() {
    return {
      showModal: false,

      movement: {
        title: "",
        amount: 0,
        description: "",
      },
      type: "",
    };
  },
  methods: {
    saveMovement(movement) {
      //Generamos el id
      movement.id = new Date().getTime();
      //Agregamos la fecha del movimiento
      movement.time = new Date();
      //Validamos si es ingreso o gasto
      this.type == "gasto" ? (movement.amount = movement.amount * -1) : "";

      this.$emit("saveMovement", movement);
      this.showModal = false;
    },
  },
};
</script>

<style scoped>
button {
  color: white;
  font-size: 1.25rem;
  background-color: var(--brand-blue);
  border: none;
  width: 100%;
  padding: 24px 60px;
  border-radius: 60px;
  box-sizing: border-box;
}

form {
  font-size: 1.24rem;
  width: 100%;
}

form .action {
  padding: 0 24px;
}

.field {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  padding: 16px 24px;
}

label {
  margin-bottom: 8px;
}

input,
textarea {
  font-size: 1.24rem;
  border: 2px solid var(--brand-blue);
  border-radius: 8px;
  padding: 8px;
}

input[type="number"] {
  text-align: right;
}

.radio-label {
  display: flex;
  align-items: center;
  margin-top: 8px;
}

.radio-label span {
  margin-top: 4px;
  margin-left: 8px;
}

input[type="radio"] {
  appearance: none;
  width: 1.24rem;
  height: 1.24rem;
  color: var(--brand-blue);
  border: 2px solid var(--brand-blue);
  border-radius: 50%;
}

input[type="radio"]:checked {
  background-color: var(--brand-blue);
}
</style>
