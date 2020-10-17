<template>
  <div class="mainTableCont">
    <table>
      <tr>
        <th>N</th>
        <th>ФИО</th>
        <th>масса / тип</th>
        <th>откуда</th>
        <th>цена</th>
        <th>Номер тел.</th>
        <th>Удалить</th>
      </tr>
      <CargoItem
        v-for="(cargo, i) of cargos"
        v-bind:cargo="cargo"
        v-bind:index="i"
        v-on:remove-cargo="removeList"
      />
    </table>
  </div>
</template>

<script>
import CargoItem from "@/components/CargoItem";
export default {
  props: ["cargos"],
  components: {
    CargoItem,
  },
  methods: {
    removeList(id) {
      this.$emit("remove-cargo", id);
    },
  },
};
</script>

<style>
table { 
  width: 100%;
  min-height: 30vw;
  padding: 2vw;
  border-collapse: collapse;
}
table td, table th {
  border: 1px solid #ddd;
  padding: 8px;
}

table tr:nth-child(even){background-color: #f2f2f2;}
table tr:hover {background-color: #ddd;}
table th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: left;
  font-size: 1vw;
  background-color: rgb(33, 75, 36);
  color: white;
}
.mainTableCont{
  overflow: auto;
}
@media (max-width: 600px) {
  th{
    font-size: 2vw;
  }
}
</style>