<template>
  <div class="login client-wrapper">
    <home-navigation />

    <div
      class="about-us-section faq"
      :style="{ backgroundImage: `url(${FILE_URL}/${banner.bannerImage})` }"
    >
      <div class="custom-container">
        <div class="hero-section">
          <h1 class="heading-21 faq">{{ banner.bannerTitle }}</h1>
        </div>
      </div>
      <div class="hero-section-cover"></div>
    </div>

    <div class="about-us-section2 login">
      <div class="custom-container">
        <div>
          <div class="div-block-27 faq">
            <div class="div-block-28">
              <img
                src="https://uploads-ssl.webflow.com/64584677a42c076b5ad19e3c/6460a0e746818cacc5ca3e96_home-icon-silhouette-svgrepo-com%201.svg"
                loading="lazy"
                alt=""
                class="image-4"
              />
            </div>
            <a href="#" class="link-block-5 w-inline-block"
              ><h1 class="heading-23">Home</h1>
              <img
                src="https://uploads-ssl.webflow.com/64584677a42c076b5ad19e3c/6460a0eddea363a6792c4285_left-arrow-next-svgrepo-com%201.svg"
                loading="lazy"
                alt=""
                class="image-5"
            /></a>
            <h1 class="heading-24">Login</h1>
          </div>
        </div>
      </div>
      <div class="div-block-29"></div>
    </div>

    <div class="login-section3">
      <div class="custom-container">
        <div class="div-block-48">
          <div class="form-block-3 w-form">
            <div class="form-3">
              <div class="form-input">
                <label for="" class="username"
                  >Username must be at least 5 characters</label
                >
                <input
                  type="text"
                  class="text-field-4 w-input"
                  maxlength="256"
                  v-model="username"
                  placeholder="Enter Username"
                  @blur="checkErrorInputs('username', username)"
                />
              </div>

              <div class="form-input">
                <label for="" class="password"
                  >Password must be at least 6 characters long</label
                >
                <input
                  type="password"
                  class="text-field-5 w-input"
                  maxlength="256"
                  name="password"
                  placeholder="Enter Password"
                  v-model="password"
                  @keypress.enter="processUserData"
                  @blur="checkErrorInputs('password', password)"
                />
              </div>
              <h1 class="heading-36">
                Forgotten password?
                <nuxt-link to="/forgotten-password">Click here</nuxt-link>
              </h1>
              <div v-if="showResponse">
                {{ response }}
              </div>

              <input
                v-if="onRequest"
                type="button"
                value="Processing..."
                class="submit-button-3 w-button stop"
              />
              <input
                v-else
                type="button"
                value="Submit"
                @click="processUserData"
                class="submit-button-3 w-button"
              />
              <h1 class="heading-36">If you don't have an account?</h1>
              <nuxt-link to="/signup" class="link-block-8 b w-inline-block"
                ><h1 class="heading-36">Sign up</h1></nuxt-link
              >
            </div>
          </div>
        </div>
      </div>
    </div>

    <home-footer />
  </div>
</template>

<script>
import HomeFooter from "../components/HomeFooter.vue";
import HomeNavigation from "../components/HomeNavigation.vue";
export default {
  data() {
    return {
      banner: "",
      username: "",
      password: "",
      complete: true,
      user: "",

      showResponse: false,
      isError: false,
      response: "",
      onRequest: false,

      isChecked: false,
      isError: false,

      usernameError: false,
      passwordError: false,
    };
  },
  methods: {
    loadScript() {
      if (!process.server) {
        let el = document.getElementById("script");

        if (el != undefined) {
          document.body.removeChild(el);
        }

        const script = document.createElement("script");
        script.type = "text/javascript";
        script.src = "/script/home.js";
        script.async = true;
        script.id = "script";
        const app = document.querySelector("#footer");
        if (app) {
          app.appendChild(script);
        } else {
          console.error("Could not find app node to append script element");
        }
      }
    },

    callResponse(msg, state) {
      this.response = msg;
      this.isError = state;
      this.showResponse = true;
      this.onRequest = false;
      setTimeout(() => {
        this.showResponse = false;
      }, 6000);
    },

    checkErrorInputs(input, data) {
      if (input == "username") {
        if (
          data == "" ||
          !data ||
          data.length < 2 ||
          !/^[a-zA-Z0-9]+$/.test(data)
        ) {
          const parent = this.$el.querySelector(".username");
          parent.classList.add("error");
          this.isError = false;
          this.usernameError = true;
          this.onRequest = false;
          return;
        } else {
          const parent = this.$el.querySelector(".username");
          parent.classList.remove("error");
          this.isError = true;
          this.usernameError = false;
        }
      } else if (input == "password") {
        if (data == "" || !data || data.length < 6) {
          const parent = this.$el.querySelector(".password");
          parent.classList.add("error");
          this.isError = true;
          this.passwordError = true;
          this.onRequest = false;
          return false;
        } else {
          const parent = this.$el.querySelector(".password");
          parent.classList.remove("error");
          this.isError = true;
          this.passwordError = false;
        }
      }
    },

    processUserData() {
      this.onRequest = true;
      this.setArray();
      this.checkArray.forEach((el) => {
        this.checkErrorInputs(el.name, el.data);
      });
      if (!this.isError) {
        return;
      }
      const form = {
        username: this.username,
        password: this.password,
      };
      this.handleLogin(form);
    },

    async handleLogin(form) {
      try {
        const result = await this.$auth.loginWith("local", { data: form });
        const user = result.data.user;
        if (user.status == "Admin") {
          this.$router.push("/admin");
        } else {
          this.$router.push("/dashboard");
        }
      } catch (err) {
        this.callResponse(err.response.data.message, true);
      }
    },

    async getBanner() {
      try {
        const result = await this.$axios.get(`/banner/?bannerCategory=Login`);
        this.banner = result.data.data[0];
      } catch (err) {
        console.log(err);
      }
    },

    setArray() {
      this.checkArray = [
        { name: "username", data: this.username },
        { name: "password", data: this.password },
      ];
    },
  },

  mounted() {
    this.getBanner();
    if (this.isAuthenticated) {
      this.$router.push("/dashboard");
    }
    this.loadScript();
  },

  computed: {
    isAuthenticated() {
      return this.$store.getters.isAuthenticated; // it check if user isAuthenticated
    },

    FILE_URL() {
      return this.$store.state.fileURL;
    },
  },

  components: { HomeNavigation, HomeFooter },
};
</script>

<style>
.form-input label {
  opacity: 0;
  transition: all 0.4s;
  font-size: 12px;
  font-weight: 200;
}

.form-input label.error {
  color: rgb(254, 50, 50);
  opacity: 1;
}
</style>
