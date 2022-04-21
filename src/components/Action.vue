<template>
  <button @click="showModal = true">Agregar movimiento</button>

  <teleport to="#app">
    <Modal v-show="showModal" @closeModal="showModal = !showModal">
      Contenido del formulario
    </Modal>
  </teleport>
</template>

<script>
import Modal from "./Modal.vue";
export default {
  components: { Modal },
  data() {
    return {
      showModal: false,
    };
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
</style>
