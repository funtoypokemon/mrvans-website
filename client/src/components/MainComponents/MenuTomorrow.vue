<template>
  <div class="custom-scrollbar menu">
    <h1>{{ title }}</h1>
    <app-food
      v-for="food in menu"
      :key="food.id"
      :name="food.name"
      :price="food.price"
      :imgLink="food.imageURL"
    ></app-food>
  </div>
</template>

<script>
import AppFood from "./Food.vue";
export default {
  data() {
    const getTomorrow = () => {
      const today = new Date();
      const tomorrow = new Date(today);
      tomorrow.setDate(tomorrow.getDate() + 1);
      let dd = String(tomorrow.getDate()).padStart(2, "0");
      let mm = String(tomorrow.getMonth() + 1).padStart(2, "0"); //January is 0!
      let yyyy = tomorrow.getFullYear();
      return dd + "/" + mm + "/" + yyyy;
    };
    return {
      title: `THỰC ĐƠN NGÀY ${getTomorrow()}`,
      menu: [],
    };
  },
  components: {
    AppFood,
  },
  created() {
    this.$http.get("/menu/tomorrow").then((res) => {
      this.menu = res.data.splice(0);
    });
  },
};
</script>

<style lang="scss">
@import "@/styles/Menu.scss";
</style>