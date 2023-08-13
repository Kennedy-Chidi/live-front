<template>
  <div class="about-us client-wrapper">
    <home-navigation />
    <div
      class="about-us-section faq"
      :style="{ backgroundImage: `url(${FILE_URL}/${banners.bannerImage})` }"
    >
      <div class="custom-container">
        <div class="hero-section">
          <h1 class="heading-21 faq">{{ banners.bannerTitle }}</h1>
          <h1 class="heading-22 faq">{{ banners.bannerSubtitle }}</h1>
        </div>
      </div>
      <div class="hero-section-cover"></div>
    </div>
    <div class="about-us-section2">
      <div class="custom-container">
        <div>
          <div class="div-block-27">
            <div class="div-block-28">
              <img
                src="https://uploads-ssl.webflow.com/64584677a42c076b5ad19e3c/6460a0e746818cacc5ca3e96_home-icon-silhouette-svgrepo-com%201.svg"
                loading="lazy"
                alt=""
                class="image-4"
              />
            </div>
            <nuxt-link to="/" class="link-block-5 w-inline-block"
              ><h1 class="heading-23">Home</h1>
              <img
                src="https://uploads-ssl.webflow.com/64584677a42c076b5ad19e3c/6460a0eddea363a6792c4285_left-arrow-next-svgrepo-com%201.svg"
                loading="lazy"
                alt=""
                class="image-5"
            /></nuxt-link>
            <h1 class="heading-24">About Us</h1>
          </div>
        </div>
      </div>
      <div class="div-block-29"></div>
    </div>
    <div class="about-us-section4">
      <div class="custom-container">
        <div>
          <h2 class="title-header about-us4">About Trade Live Limited</h2>
          <div class="div-block-33">
            <div class="div-block-34">
              <div class="heading-25" v-html="about.content"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="about-us-section3">
      <div class="custom-container">
        <div class="div-block-30">
          <div class="buy-crypto-left about-us3">
            <h2 class="title-header left about-us3">
              {{ firstBlog.title }}
            </h2>
            <div
              v-if="firstBlog.content"
              class="text-custom about-us3"
              v-html="`${firstBlog.content.substring(0, 600)}...`"
            ></div>
            <nuxt-link
              :to="`/news-details/${firstBlog._id}`"
              class="hero-button about-us3 w-button"
              >Read More</nuxt-link
            >
          </div>
          <div class="div-block-32">
            <img
              :src="`${FILE_URL}/${firstBlog.banner}`"
              loading="lazy"
              sizes="(max-width: 479px) 96vw, (max-width: 680px) 94vw, (max-width: 767px) 640px, (max-width: 991px) 46vw, (max-width: 1279px) 47vw, (max-width: 1439px) 43vw, 40vw"
              :srcset="`${FILE_URL}/${firstBlog.banner} 500w,
                ${FILE_URL}/${firstBlog.banner}       640w
              `"
              alt=""
            />
          </div>
        </div>
      </div>
    </div>

    <div class="about-us-section5">
      <div class="div-block-37">
        <div class="div-block-36">
          <h1 class="heading-26">Our Clients Stats</h1>
          <h1 class="heading-27">
            We are happy to show you our membership figures, how our membership
            has increased to this figures since we started has been due to our
            consistent daily profits over the years.<br />
          </h1>
          <div class="div-block-39">
            <div class="div-block-38">
              <h1 class="heading-28">
                {{ formatMoney(company.totalMembers) }}
              </h1>
              <h1 class="heading-29">TOTAL MEMBERS</h1>
            </div>
            <div class="div-block-38">
              <h1 class="heading-28">
                {{ formatMoney(company.activeMembers) }}
              </h1>
              <h1 class="heading-29">ACTIVE MEMBERS</h1>
            </div>
            <div class="div-block-38">
              <h1 class="heading-28">
                {{ formatMoney(company.onlineMembers) }}
              </h1>
              <h1 class="heading-29">ONLINE MEMBERS</h1>
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
      banners: "",
      about: "",
      company: "",
      firstBlog: "",
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

    formatMoney(amount) {
      if (amount == "" || amount == null || amount == undefined) {
        return "0.00";
      } else {
        return amount.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
      }
    },

    async getCompany() {
      try {
        const result = await this.$axios.get(`/company`);
        this.company = result.data.data;
      } catch (err) {
        console.log(err);
      }
    },

    async getBlogs() {
      try {
        const result = await this.$axios.get("/blog");
        this.firstBlog = result.data.data[0];
      } catch (err) {
        console.log(err.response);
      }
    },

    async getBanner() {
      try {
        const result = await this.$axios.get(`/banner/?bannerCategory=About`);
        this.banners = result.data.data[0];
      } catch (err) {
        console.log(err);
      }
    },

    async getAbout() {
      try {
        const result = await this.$axios.get(`/about`);
        this.about = result.data.data[0];
      } catch (err) {
        console.log(err);
      }
    },
  },
  mounted() {
    this.getBanner();
    this.getAbout();
    this.getBlogs();
    this.getCompany();
    this.loadScript();
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
.heading-25,
.div-block-34 {
  width: 100%;
}

.title-header.about-us4 {
  margin-top: 30px;
  text-align: left;
  margin-bottom: 20px;
}
</style>
