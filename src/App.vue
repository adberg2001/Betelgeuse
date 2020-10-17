<template>
  <div id="app">
    <header>
      <span class="logo_text">Betelgeuse</span>
      <img class="logo" src="@/images/road.png" alt="" />
    </header>
    <section 
    :style="{ backgroundImage: `url(${bg})` }"
    class="desc">
      <div class="desc_bgColor">
        <h1 class="desc_title">
          Доставка грузов из Европы и стран СНГ в Кыргызстан от 5 тонн на грузовом транспорте
        </h1>
      </div>
    </section>
    <section class="services">
      <h2 class="services-title">Наши услуги</h2>
      <div class="services_cont">
        <div class="services_cell">
          <img class="services_logo" src="https://static.tildacdn.com/tild6332-6465-4430-b235-646232346636/Tilda_Icons_43_logis.svg" alt="">
          <h3 class="services_cell_title">Сборные грузы</h3>
          <span class="services_cell_desc">
            Если у вас есть небольшая партия товара, сырья или оборудования мы, сможем доставить ваш груз от двери до двери.
          </span>
        </div>
        <div class="services_cell">
          <img class="services_logo" src="https://static.tildacdn.com/tild6332-6465-4430-b235-646232346636/Tilda_Icons_43_logis.svg" alt="">
          <h3 class="services_cell_title">Сборные грузы</h3>
          <span class="services_cell_desc">
            Если у вас есть небольшая партия товара, сырья или оборудования мы, сможем доставить ваш груз от двери до двери.
          </span>
        </div>
        <div class="services_cell">
          <img class="services_logo" src="https://static.tildacdn.com/tild6332-6465-4430-b235-646232346636/Tilda_Icons_43_logis.svg" alt="">
          <h3 class="services_cell_title">Сборные грузы</h3>
          <span class="services_cell_desc">
            Если у вас есть небольшая партия товара, сырья или оборудования мы, сможем доставить ваш груз от двери до двери.
          </span>
        </div>
        <div class="services_cell">
          <img class="services_logo" src="https://static.tildacdn.com/tild6332-6465-4430-b235-646232346636/Tilda_Icons_43_logis.svg" alt="">
          <h3 class="services_cell_title">Сборные грузы</h3>
          <span class="services_cell_desc">
            Если у вас есть небольшая партия товара, сырья или оборудования мы, сможем доставить ваш груз от двери до двери.
          </span>
        </div>
      </div>
    </section>
    <AddCargo @add-cargo="addCargo" />
    <Loader v-if="loading" />
    <CargoList
      v-else-if="cargos.length"
      v-bind:cargos="cargos"
      @remove-cargo="removeList"
    />
    <p class="empty" v-else>Заказов нет!</p>
  </div>
</template>


<script>
import CargoList from "@/components/CargoList";
import AddCargo from "@/components/AddCargo";
import Loader from "@/components/Loader";
import bg from "@/images/wallpaper.jpg"
export default {
  name: "app",
  data() {
    return {
      cargos: [
        {id: 1, mass: "20", pointA: "Европа", first_name: "Султан", last_name: "Сулайманов", type_of_cargo: "Наливной", phone: "+996-775-607-075", selected: false},
        {id: 2, mass: "25", pointA: "СНГ", first_name: "Мурат", last_name: "Садыров", type_of_cargo: "Сыпучий", phone: "+996-775-607-075", selected: false},
        {id: 3, mass: "18", pointA: "СНГ", first_name: "Урмат", last_name: "Шаршенов", type_of_cargo: "Взрывоопасный", phone: "+996-775-607-075", selected: false},
        {id: 4, mass: "20", pointA: "СНГ", first_name: "Мухтар", last_name: "Мукашев", type_of_cargo: "Длинномерный", phone: "+996-775-607-075", selected: false},
        {id: 5, mass: "15", pointA: "Европа", first_name: "Султан", last_name: "Сулайманов", type_of_cargo: "Взрывоопасный", phone: "+996-775-607-075", selected: false},
      ],
      loading: true,
      filter: "all",
      bg: bg,
    };
  },
  mounted() {
        setTimeout(() => {
          this.loading = false;
        }, 1000);
  },
  methods: {
    removeList(id) {
      this.cargos = this.cargos.filter((t) => t.id !== id);
    },
    addCargo(newCargo) {
      this.cargos.push(newCargo);
    },
  },
  components: {
    CargoList,
    AddCargo,
    Loader,
  },
};
</script>

<style>
body{
  margin: 0;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: rgb(9, 32, 11);
}

header{
  display: flex;
  align-items: center;
  padding: 1.5vw 30px 10px;
}

.logo{
  height: 60px;
  object-fit: contain;
  margin-left: -90px;
}
.logo_text{
  line-height: 19px;
  font-size: 12px;
  font-weight: 600;
}
.desc{
  height: 40vw;
  background-position: center;
  background-size: cover;
}
.desc_bgColor{
  height: 100%;
  background: rgba(3, 48, 9, 0.479);
  padding: 0 15vw;
  display: flex;
  align-items: center;
}

.desc_title{
  color: white;
  text-align: center;
  font-weight: 400;
  font-size:3.5vw;
}

.services{
  background: rgba(198, 238, 198, 0.685);
}

.services-title{
  margin: 0;
  padding: 3vw 0;
  font-size: 2vw;
}

.services_cont{
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-row-gap: 1vw;
  grid-column-gap: 1vw;
  padding: 2vw;
}

@media (max-width: 800px) {
  .services_cont{
  grid-template-columns: 1fr;
}
}

.services_cell{
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-self: center;
  background: #fff;
  border-radius: 4px;
  padding: 3vw;
}

.services_logo{
  height: 6vw;
  object-fit: contain;
}

.services_cell_title{
  font-size: 2.0vw;
  margin: 9px 0;
}

.services_cell_desc{
  font-size: 1.2vw;
  text-align: start;
}
.empty{
  height: 30vw;
  display: flex;
  font-size: 3vw;
  margin: 0;
  align-items: center;
  justify-content: center;
}
</style>
