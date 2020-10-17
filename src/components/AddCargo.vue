<template>
  <section :style="{ backgroundImage: `url(${actrosBg})` }" class="formCont">
    <form @submit.prevent="onSubmit">
      <input placeholder="Имя" type="text" v-model="first_name" />
      <input placeholder="Фамилия" type="text" v-model="last_name" />

      <select v-model="type_of_cargo">
        <option value="" disabled selected hidden>Выберите тип груза...</option>
        <option value="Наливной">Наливной</option>
        <option value="Сыпучий">Сыпучий</option>
        <option value="Взрывоопасный">Взрывоопасный</option>
        <option value="Длинномерный">Длинномерный</option>
      </select>

      <input type="number" required placeholder="Масса (т)"  v-model="mass" />

      <select required v-model="pointA">
        <option value="" disabled selected hidden>Выберите Откуда...</option>
        <option value="СНГ">СНГ</option>
        <option value="Европа">Европа</option>
      </select>

      <input required placeholder="Номер тел." type="number" v-model="phone" />

      <button type="submit">Добавить</button>
    </form>
  </section>
</template>

<script>
import actrosBg from "@/images/form_img_track.jpg";
export default {
  data() {
    return {
      mass: "",
      pointA: "",
      type_of_cargo: "",
      phone: "",
      first_name: "",
      last_name: "",
      actrosBg: actrosBg,
    };
  },
  methods: {
    onSubmit() {
      if (this.mass.trim()) {
        const newCargo = {
          id: Date.now(),
          mass: this.mass,
          pointA: this.pointA,
          type_of_cargo: this.type_of_cargo,
          phone: this.phone,
          first_name: this.first_name,
          last_name: this.last_name,
          selected: false
        };

        this.$emit("add-cargo", newCargo);
        this.type_of_cargo = "";
        this.mass = "";
        this.phone = "";
        this.first_name = "";
        this.last_name = "";
        this.pointA = "";
      }
    },
  },
};
</script>

<style scoped>
.formCont {
  min-height: 40vw;
  display: flex;
  background-position: center;
  background-size: cover;
}

form {
  min-height: 30vh;
  width: 100%;
  display: grid;
  grid-template-rows: repeat(7, 1fr);
  grid-row-gap: 0.5vw;
  padding: 8vw 5vw;
  margin-left: 40vw;
}

input {
  background: rgba(0, 0, 0, 0.486);
  color: #fff;
  font-size: 18px;
  border: none;
  font-size: 1vw;
}
select {
  background-color: rgba(0, 0, 0, 0.486);
  color: #fff;
  font-size: 1vw;
  border: none;
}
::placeholder {
  color: #fff;
  font-size: 1vw;
}
button{
  width: 30%;
  background: rgb(33, 75, 36);
  color: #fff;
  border: none;
  font-size: 1vw;
}
@media (max-width: 600px) {
form {
  grid-row-gap: 1vw;
  padding: 8vw 1.5vw;
  margin-left: 40vw;
}
input {
  font-size: 1.9vw;
}
select {
  font-size: 1.9vw;
}
::placeholder {
  font-size: 1.9vw;
}
button{
  width: 50%;
  font-size: 8px;
}
}

</style>