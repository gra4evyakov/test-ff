<template>
  <div class="home">
    <img src="@/assets/images/logo-2.png" alt="logo" id="homeLogo" />
    <div class="home__buttons-wrapper hidden" ref="buttonWrapper">
      <div>
        <router-link to="/showcase">
          <button class="btn">Заказать</button>
        </router-link>
        <router-link v-if="user" to="/profile">
          <button class="btn">Профиль</button>
        </router-link>
        <router-link v-else to="/auth">
          <button class="btn">Войти</button>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from "vuex";

export default {
  name: "HomePage",

  mounted() {
    const logo = document.getElementById("homeLogo"),
      homeButtonsWrapper = this.$refs.buttonWrapper;

    setTimeout(() => {
      logo.style.width = "30%";
      logo.style.top = "30px";
      logo.style.marginTop = "30px";

      homeButtonsWrapper.style.visibility = "visible";
      homeButtonsWrapper.style.opacity = "1";
      homeButtonsWrapper.style.bottom = "10%";
    }, 0);
  },
  computed: {
    ...mapState(["user"]),
  },
};
</script>

<style scoped>
.home {
  height: 100vh;
  text-align: center;

  background-image: linear-gradient(rgba(255, 164, 0, 0.5), rgba(0, 0, 0, 0.5)),
    url("../assets/images/home-bg.jpeg");
  background-position: center;
  background-size: cover;
}

#homeLogo {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
  margin-top: 100px;
  max-width: 400px;
  width: 80%;
  transition: opacity 1s, width 1s 0s, margin-top 1s 0.8s;
}

.home__buttons-wrapper {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  margin: 0 auto;
  transition: all 1s 1s;
}

button {
  display: block;
  margin: 10px auto;
  padding: 20px 40px;
  width: 250px;
  font-weight: 500;
}
</style>
