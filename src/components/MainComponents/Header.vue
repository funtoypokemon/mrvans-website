<template>
  <div id="header">
    <img @click="componentName='app-home'" id="logo" src="@/assets/Logo.svg" alt />
    <nav class="desktop">
      <li @click="componentName='app-home'">
        <a>TRANG CHỦ</a>
      </li>
      <div>
        <li
          class="dropdown"
          @mouseenter="menuHover = true"
          @mouseleave="menuHover = false"
          @click="componentName='app-menu-today'"
        >MENU</li>
        <ul
          class="dropdown-content"
          v-if="turnOnMenuHover"
          @mouseenter="menuChildHover = true"
          @mouseleave="menuChildHover = false"
        >
          <li @click="componentName='app-menu-today'">
            <a>THỰC ĐƠN HÔM NAY</a>
          </li>
          <br />
          <li @click="componentName='app-menu-tomorrow'">
            <a>THỰC ĐƠN NGÀY MAI</a>
          </li>
        </ul>
      </div>
      <div>
        <li
          class="dropdown"
          id="product-dropdown"
          @mouseenter="productHover=true"
          @mouseleave="productHover = false"
          @click="componentName='app-product'"
        >SẢN PHẨM</li>
        <ul
          class="dropdown-content"
          id="product-content"
          v-if="turnOnProductHover"
          @mouseenter="productChildHover=true"
          @mouseleave="productChildHover = false"
        >
          <li
            v-for="product in products"
            :key="product.id"
            @click="componentName=`app-product-${product.id}`"
          >
            <a>{{ product.name }}</a>
          </li>
        </ul>
      </div>

      <li @click="componentName='app-whyus'">
        <a>VÌ SAO CHỌN CHÚNG TÔI</a>
      </li>
      <li @click="componentName='app-contact'">
        <a>LIÊN HỆ</a>
      </li>
    </nav>
    <ul class="desktop">
      <li>
        <img
          onclick="window.open('https://www.facebook.com/comvanphongmrvans/','_blank')"
          src="@/assets/icons/facebook.png"
          alt
          title="https://www.facebook.com/comvanphongmrvans/"
        />
      </li>
      <li>
        <img src="@/assets/icons/zalo.png" alt title="0368680611" />
      </li>
      <li>
        <img src="@/assets/icons/phone.png" alt="0564646499" title="0564646499" />
      </li>
    </ul>
    <div class="mobile hamburger-wrapper">
      <button class="hamburger" @click.stop="hamburgerOpen">
        <span></span>
        <span></span>
        <span></span>
      </button>
      <app-navbar style="z-index:1000" v-show="hamburgerClicked" :products="products"></app-navbar>
    </div>
  </div>
</template>

<script>
import AppNavbar from "./Navbar.vue";
import { eventBus } from "@/main";
export default {
  data() {
    return {
      hamburgerClicked: false,
      menuHover: false,
      menuChildHover: false,
      productHover: false,
      productChildHover: false,
      componentName: "app-home",
      products: [],
    };
  },
  methods: {
    hamburgerOpen() {
      this.hamburgerClicked = !this.hamburgerClicked;
    },
  },
  computed: {
    turnOnMenuHover() {
      return !((this.menuHover === false) & (this.menuChildHover === false));
    },
    turnOnProductHover() {
      return !(
        (this.productHover === false) &
        (this.productChildHover === false)
      );
    },
  },
  watch: {
    componentName() {
      eventBus.$emit("pageChanged", this.componentName);
    },
  },
  components: {
    AppNavbar,
  },
  created() {
    eventBus.$on("closeSidebar", () => {
      this.hamburgerClicked = false;
    });
    this.$http.get("/products").then((response) => {
      if (response.data.length !== 0) this.products = response.data.splice(0);
    });
  },
};
</script>

<style lang="scss" scoped >
@import "@/styles/Header.scss";
</style>
