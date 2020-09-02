<template>
  <footer>
    <address>
      <h4>Địa chỉ: 236/3 Hẽm 236 Nguyễn Thái Bình, Phường 12, Quận Tân Bình, Tp. Hồ Chí Minh</h4>
      <p id="phone">Đặt món ngay: 05 646464 99</p>
      <p id="phone">Hotline CSKH: 03 686806 11</p>
      <p id="email">
        Email:
        <a href="mailto:phumrvans@gmail.com">phumrvans@gmail.com</a>
      </p>
    </address>
    <!-- Load Facebook SDK for JavaScript -->
    <div id="fb-root"></div>
    <div
      class="fb-customerchat"
      attribution="setup_tool"
      page_id="109226167490414"
      theme_color="#0084ff"
    ></div>
  </footer>
</template>
<script>
export default {
  mounted() {
    window.fbAsyncInit = function () {
      // eslint-disable-next-line
      FB.init({
        xfbml: true,
        version: "v7.0",
      });
    };
  },
}
</script>
<style lang="scss">
footer {
  width: 100%;
  height: 10vh;
  background-color: #333333;
  color: white;
  font-size: 2vh;
  position: fixed;
  bottom: 0;
}
address {
  width: 100%;
  p,
  h4 {
    font-size: 1.5vh;
    margin-left: 10px;
    margin-top: 5px;
    margin-bottom: 0;
  }
}
#email {
  a {
    font-style: italic;
    color: white;
  }
}
</style>
