<template>
  <div class="blog">
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

    <div class="about-us-section2 create-account">
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
            <h1 class="heading-24">Terms</h1>
          </div>
        </div>
      </div>
      <div class="div-block-29"></div>
    </div>

    <div class="blog-section3">
      <div class="custom-container">
        <div class="div-block-49">
          <div class="div-block-50">
            <div class="div-block-57">
              <div>
                <h1 class="heading-42">{{ terms.heading }}</h1>
                <h1 class="heading-43" v-html="terms.content"></h1>
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
      terms: "",
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

    async getBanner() {
      try {
        const result = await this.$axios.get(`/banner/?bannerCategory=Terms`);
        this.banner = result.data.data[0];
      } catch (err) {
        console.log(err);
      }
    },

    async getTerms() {
      try {
        const result = await this.$axios.get("/terms");
        this.terms = result.data.data[0];
      } catch (err) {
        console.log(err.response.data.message);
      }
    },
  },
  mounted() {
    this.loadScript();
    this.getBanner();
    this.getTerms();
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
.div-block-50 {
  width: 100%;
}
</style>
