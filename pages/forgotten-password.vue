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
                <label for="" class="email">Please enter a valid email</label>
              </div>
              <input
                type="text"
                class="text-field-4 w-input"
                maxlength="256"
                v-model="email"
                placeholder="Enter Email"
                @keypress.enter="processUserData"
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

              <div class="link-block-8 w-inline-block">
                <h1 class="heading-36 forgotten-password">
                  <strong
                    >Already have an account?,
                    <nuxt-link to="/login" class="terms"
                      >Login</nuxt-link
                    ></strong
                  >
                </h1>
              </div>
              <div class="link-block-8 w-inline-block">
                <h1 class="heading-36 forgotten-password">
                  If you don&#x27;t have an account,
                  <nuxt-link to="/signup" class="terms"
                    >create an account</nuxt-link
                  >
                </h1>
              </div>
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
      email: "",

      showResponse: false,
      isError: false,
      response: "",
      onRequest: false,
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

    checkErrorInputs(input, data) {
      if (input == "email") {
        if (data == "" || !data || !/^\S+@\S+\.\S+$/.test(data)) {
          const parent = this.$el.querySelector(".email");
          parent.classList.add("active");
          this.isError = false;
          return;
        } else {
          const parent = this.$el.querySelector(".email");
          parent.classList.remove("active");
          this.isError = true;
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

    processUserData() {
      this.onRequest = true;
      this.setArray();
      this.checkArray.forEach((el) => {
        this.checkErrorInputs(el.name, el.data);
      });
      if (!this.isError) {
        return;
      }
      this.processEmail();
    },

    async processEmail() {
      const form = {
        email: this.email,
      };

      try {
        await this.$axios.patch(`/users/forgotten-password`, form);
        this.callResponse(
          "Please verify your email and click on the link button to continue.",
          false
        );
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
      this.checkArray = [{ name: "email", data: this.email }];
    },
  },
  mounted() {
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
