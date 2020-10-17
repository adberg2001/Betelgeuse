<template>
  <tr v-bind:class="{ selected: cargo.selected }">
    <td v-on:click="cargo.selected = !cargo.selected">
      <strong>{{ index + 1 }}</strong>
    </td>
    <td class="long" v-on:click="cargo.selected = !cargo.selected">
      {{ (cargo.first_name + " " + cargo.last_name) | uppercase }}
    </td>
    <td v-on:click="cargo.selected = !cargo.selected">
      {{ cargo.mass ? cargo.mass + "т" : "не указана" }} /
      {{ cargo.type_of_cargo ? cargo.type_of_cargo : "не указано" }}
    </td>
    <td v-on:click="cargo.selected = !cargo.selected">
      {{ cargo.pointA ? cargo.pointA : "Не указан" }}
    </td>
    <td v-on:click="cargo.selected = !cargo.selected">{{ cargo | calc }} USD</td>
    <td class="long" v-on:click="cargo.selected = !cargo.selected">
      {{ cargo.phone }}
    </td>
    <td>
      <button class="rm" v-on:click="$emit('remove-cargo', cargo.id)">
        &times;
      </button>
    </td>
  </tr>
</template>

<script>
export default {
  props: {
    cargo: {
      type: Object,
      required: true,
    },
    index: Number,
  },
  filters: {
    uppercase(value) {
      return value.toUpperCase();
    },
    calc(cargo) {
      if (cargo) {
        const priceForPointA = cargo.pointA === "СНГ" ? 8 : 14;
        const priceForMass = cargo.mass;
        const proceForType =
          cargo.type_of_cargo === "Наливной"
            ? 18
            : cargo.type_of_cargo === "Сыпучий"
            ? 15
            : cargo.type_of_cargo === "Взрывоопасный"
            ? 22
            : 12;
        console.log(priceForPointA, priceForMass, proceForType);
        const total = priceForPointA * priceForMass * proceForType;
        return total;
      }
    },
  },
};
</script>

<style scoped>
td {
  width: auto;
  font-size: 1vw;
}
.rm {
  width: 1vw;
  height: 1vw;
  background: red;
  color: #fff;
  border-radius: 50%;
  font-weight: bold;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto;
  border: none;
  z-index: 99;
}

input {
  margin-right: 1rem;
}
.selected {
  background: rgba(0, 0, 0, 0.657);
  color: #fff;
}
@media (max-width: 600px) {
  td {
    font-size: 1.9vw;
  }
  .rm {
  width: 15px;
  height: 15px;
}
}
</style>