<template>
  <div>
    <HeaderPart />

    <Transition>
      <div class="wrapper" v-if="isShowAuthBlock">
        <h3 class="text-center">Авторизация</h3>
        <form>
          <div>
            <input type="text" v-model.trim="loginInput" placeholder="Логин (user или manager)" />
          </div>

          <div>
            <input type="password" placeholder="Пароль (user или manager)" v-model.trim="passwordInput" />
          </div>

          <button class="btn" @click.prevent="authUser">Войти</button>
        </form>
      </div>

      <div class="wrapper" v-else>
        <h3 class="text-center">Регистрация</h3>
        <form>
          <div>
            <input type="text" name="login" id="newlogin" placeholder="Логин (user или manager)" />
          </div>

          <div>
            <input type="password" name="password" id="newpassword" placeholder="Пароль (user или manager)" />
          </div>

          <button class="btn">Регистрация</button>
        </form>
        <div class="reg-block">
          <p>Или войти, если уже ага</p>
          <button class="btn" @click="isShowAuthBlock = true">Войти</button>
        </div>
      </div>
    </Transition>

    <FooterPart />
  </div>
</template>

<script>
import HeaderPart from "@/views/parts/HeaderPart";
import FooterPart from "@/views/parts/FooterPart";
import { mapActions, mapState } from "vuex";
import router from "@/router";

export default {
  name: "LoginPage",
  components: {
    HeaderPart,
    FooterPart,
  },
  data() {
    return {
      isShowAuthBlock: true,
      loginInput: "",
      passwordInput: "",
    };
  },
  methods: {
    ...mapActions(["loginSubmit"]),
    authUser: function () {
      let params = {
        login: this.loginInput,
        password: this.passwordInput,
      };
      this.loginSubmit(params);
    },
  },
  computed: {
    ...mapState(["user"]),
  },
  beforeMount() {
    if (this.user) router.push("/");
  },
};
</script>

<style scoped>
form,
.reg-block {
  max-width: 400px;
  margin: 0 auto;
}

label {
  color: white;
}

input {
  width: 100%;
  padding: 3px;
  border: none;
  border-bottom: 1px solid grey;
  background: transparent;
  color: grey;
  outline: none;
  font-size: 1.2rem;
  margin: 10px 0;
}

input:last-child {
  margin-bottom: 2rem;
}

.v-leave-active {
  transition: opacity 0.4s ease;
}

.v-enter-active {
  transition: opacity 0.4s ease 0.4s;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>
