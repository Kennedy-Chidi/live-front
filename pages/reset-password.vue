<template>
  <div class="forgotten-password">
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
            <h1 class="heading-24">Recover Account</h1>
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
              <div>
                <label for="" class="password"
                  >Please enter a strong valid password.</label
                >
              </div>
              <input
                type="password"
                class="text-field-4 w-input"
                maxlength="256"
                v-model="password"
                placeholder="Enter Password"
                @blur="checkErrorInputs('password', password)"
              />
              <div>
                <label for="" class="cPassword"
                  >Please enter a password that match.</label
                >
              </div>
              <input
                type="password"
                class="text-field-4 w-input"
                maxlength="256"
                v-model="cPassword"
                @blur="checkErrorInputs('cPassword', cPassword)"
                placeholder="Confirm Password"
              />

              <div v-if="showResponse">
                {{ response }}
              </div>

              <input
                v-if="onRequest"
                type="button"
                value="Processing..."
                class="submit-button-3 w-button"
              />

              <input
                v-else
                type="button"
                value="Login"
                data-wait="Please wait..."
                @click="processUserData"
                class="submit-button-3 w-button"
              />
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
      cPassword: "",
      password: "",
      complete: true,
      user: "",
      company: "",
      banner: "",

      showResponse: false,
      isError: false,
      response: "",
      onRequest: false,

      isError: false,
      passwordError: false,
      cPasswordError: false,
    };
  },
  methods: {
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
      if (input == "password") {
        if (data == "" || !data || data.length < 6) {
          const parent = this.$el.querySelector(".password");
          parent.classList.add("error");
          this.isError = false;
          this.passwordError = true;
          this.onRequest = false;
          return false;
        } else {
          const parent = this.$el.querySelector(".password");
          parent.classList.remove("error");
          this.isError = true;
          this.passwordError = false;
        }
      } else if (input == "cPassword") {
        if (!data || data != this.password) {
          const parent = this.$el.querySelector(".cPassword");
          parent.classList.remove("error");
          this.isError = false;
          this.cPasswordError = true;
        } else {
          const parent = this.$el.querySelector(".cPassword");
          parent.classList.remove("error");
          this.isError = true;
          this.cPasswordError = false;
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
      this.processPassword();
    },

    setArray() {
      this.checkArray = [
        { name: "password", data: this.password },
        { name: "cPassword", data: this.cPassword },
      ];
    },

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

    async processPassword() {
      const form = {
        password: this.password,
        cPassword: this.cPassword,
      };

      try {
        await this.$axios.patch(
          `/users/reset-password/${this.$route.query.token}`,
          form
        );
        this.cPassword = "";
        this.password = "";
        this.callResponse(
          "Your password has been reset successfully, kindly login to continue.",
          false
        );
      } catch (err) {
        this.callResponse(err.response.data.message, true);
      }
    },

    async getCompany() {
      try {
        const result = await this.$axios.get("/company");
        this.company = result.data.data;
      } catch (err) {
        console.log(err.response.data);
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
  },
  mounted() {
    this.getCompany();
    this.loadScript();
    this.getBanner();
  },
  computed: {
    FILE_URL() {
      return this.$store.state.fileURL;
    },
  },
  components: { HomeNavigation, HomeFooter },
};
</script>

<style>
a.terms {
  font-weight: bold;
  color: #ffb426;
}
</style>
