<template>
  <Layout>
    <template #header>
      <Header />
    </template>
    <template #resume>
      <Resume
        :label="'Ahorro total'"
        :date="date"
        :amount="amount"
        :total-amount="200000"
      >
        <template #graphic>
          <Graphic :amounts="amounts" />
        </template>

        <template #action>
          <Action @saveMovement="addMovement" />
        </template>
      </Resume>
    </template>
    <template #movements>
      <Movements :movements="movements" @remove="remove" />
    </template>
  </Layout>
</template>

<script>
import Layout from "./Layout.vue";
import Header from "./Header.vue";
import Resume from "./Resume/Index.vue";
import Graphic from "./Resume/Graphic.vue";
import Movements from "./Movements/Index.vue";
import Action from "./Action.vue";

export default {
  components: {
    Layout,
    Header,
    Resume,
    Graphic,
    Movements,
    Action,
  },

  computed: {
    amounts() {
      const lastDays = this.movements
        .filter((m) => {
          const today = new Date();
          const oldDate = today.setDate(today.getDate() - 30);

          return m.time > oldDate;
        })
        .map((m) => m.amount);

      return lastDays.map((m, i) => {
        const lastMovements = lastDays.slice(0, i);

        return lastMovements.reduce((addition, movement) => {
          return addition + movement;
        }, 0);
      });
    },
  },

  data() {
    return {
      amount: 100,
      /*  amounts: [100, 200, 500, 200, -400, -600, 0, 300, 500, 500], */
      date: "26 de noviembre del 2022",
      movements: [
        {
          id: 1,
          title: "Movimiento",
          description: "Deposito de salario",
          amount: 100,
          time: new Date("2022-03-10"),
        },
        {
          id: 2,
          title: "Movimiento 1",
          description: "Deposito de honorarios",
          amount: 200,
          time: new Date("2022-03-12"),
        },
        {
          id: 3,
          title: "Movimiento 3",
          description: "Comida",
          amount: 510,
          time: new Date("2022-04-10"),
        },
        {
          id: 4,
          title: "Movimiento 4",
          description: "Colegiatura",
          amount: 200,
          time: new Date("2022-04-13"),
        },
        {
          id: 5,
          title: "Movimiento 5",
          description: "Reparación equipo",
          amount: -400,
          time: new Date("2022-04-13"),
        },
        {
          id: 6,
          title: "Movimiento 6",
          description: "Reparación equipo",
          amount: -600,
          time: new Date("2022-04-15"),
        },
        {
          id: 7,
          title: "Movimiento 7",
          description: "Reparación equipo",
          amount: 20,
          time: new Date("2022-04-18"),
        },
        {
          id: 8,
          title: "Movimiento 8",
          description: "Reparación equipo",
          amount: 300,
          time: new Date("2022-04-19"),
        },
        {
          id: 9,
          title: "Movimiento 9",
          description: "Reparación equipo",
          amount: 530,
          time: new Date("2022-04-22"),
        },
        {
          id: 10,
          title: "Movimiento 10",
          description: "Reparación equipo",
          amount: 550,
          time: new Date("2022-04-23"),
        },
      ],
    };
  },
  methods: {
    addMovement(movement) {
      /* console.log(movement); */
      this.movements.push(movement);
    },
    remove(id) {
      let index = this.movements.findIndex((movement) => movement.id === id);
      this.movements.splice(index, 1);
    },
  },
};
</script>

<style></style>
