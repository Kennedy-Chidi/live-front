<template>
  <div class="page faq">
    <div class="scroll-up">
      <img
        src="https://uploads-ssl.webflow.com/6458b19446eea345a074cdaf/645a57fff24418be062a10b3_line-angle.svg"
        loading="lazy"
        alt=""
        class="scroll-icon"
      />
    </div>
    <div class="landing">
      <home-navigation />
      <div class="landing-flex full login">
        <div class="cover"></div>
        <div class="custom-container login">
          <div class="signed">
            Home / <span class="text-span-6">Aurhtorization</span>
          </div>
          <h1 class="main-title login" v-if="onRequest">Activating Account</h1>
          <h1 class="main-title login" v-else>Activation Successful</h1>
        </div>
      </div>
    </div>
    <div class="custom-container">
      <div class="blog-body full login">
        <div class="each-question-section">
          <h1 class="main-title quest" v-if="onRequest">
            Waiting for response...
          </h1>
          <div class="each-faq terms">
            <div class="sign-label answer" v-if="onRequest">
              Kindly exercise patience while our system process your account for
              activation to start your Journey with
              {{ company.companyName }} experience.
            </div>
            <div class="sign-label answer" v-else>
              Congratulatons... Your account has been successfully activated,
              kindly <nuxt-link to="/login">Login</nuxt-link> to continue your
              journey with {{ company.companyName }}
            </div>
          </div>
        </div>
        <div class="radial-gradient"></div>
      </div>
    </div>
    <home-footer />
  </div>
</template>

<script>
import HomeNavigation from "../components/HomeNavigation.vue";
export default {
  data() {
    return {
      response: "",
      isError: false,
      showResponse: false,
      onRequest: false,
      status: false,

      company: "",
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

    async activateUser(id) {
      try {
        const result = await this.$axios.patch(`/users/activate-user/${id}`, {
          suspension: false,
        });
        this.status = true;
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
  },
  mounted() {
    // this.loadScript();
    this.getCompany();
    if (this.$route.query.token) {
      this.activateUser(this.$route.query.token);
    } else {
      this.$router.push("/signup");
    }
  },
  computed: {
    isAuthenticated() {
      return this.$store.getters.isAuthenticated; // it check if user isAuthenticated
    },
  },
  components: { HomeNavigation },
};
</script>

<style HomeFooter></style>
