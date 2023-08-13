<template>
  <div class="faq client-wrapper">
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
            <h1 class="heading-24">FAQ</h1>
          </div>
        </div>
      </div>
      <div class="div-block-29"></div>
    </div>

    <div class="faq-section3">
      <div class="custom-container">
        <div v-if="faqCategories" class="div-block-43">
          <div
            v-for="category in faqCategories"
            :key="category._id"
            class="div-block-40"
          >
            <div class="div-block-41">
              <h1 class="heading-30">{{ category }}</h1>
              <div class="line faq"></div>
            </div>
            <div
              v-for="faq in filteredFAQ(category)"
              :key="faq._id"
              class="div-block-42"
            >
              <div
                class="link-block-6 w-inline-block"
                @click="toggleQuestion(faq)"
              >
                <h1 class="heading-32">{{ faq.question }}</h1>
                <img
                  src="https://uploads-ssl.webflow.com/64584677a42c076b5ad19e3c/6460d8ce5d6484a79c81d21d_down-arrow-backup-2-svgrepo-com%201%20(1).svg"
                  loading="lazy"
                  alt=""
                  class="image-6"
                />
              </div>
              <div v-if="faq.checked">
                <div class="heading-33" v-html="faq.answer"></div>
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
      faqs: [],
      faqCategories: [],
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

    filteredFAQ(data) {
      return this.faqs.filter((item) => item.category === data);
    },

    getFaqCategories(data) {
      this.faqCategories = [...new Set(data.map((item) => item.category))];
    },

    toggleQuestion(question) {
      this.checkFAQs(this.faqs);
      question.checked = !question.checked;
    },

    checkFAQs(data) {
      data.forEach((el) => {
        el.checked = false;
      });
      return data;
    },

    async getFaqs() {
      try {
        const result = await this.$axios.get("/faq/?limit=60");
        this.getFaqCategories(result.data.data);
        this.faqs = await this.checkFAQs(result.data.data);
      } catch (err) {
        console.log(err.response.data.message);
      }
    },

    async getBanner() {
      try {
        const result = await this.$axios.get(`/banner/?bannerCategory=FAQ`);
        this.banner = result.data.data[0];
      } catch (err) {
        console.log(err);
      }
    },
  },
  mounted() {
    this.loadScript();
    this.getBanner();
    this.getFaqs();
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
.link-block-6.w-inline-block {
  cursor: pointer;
}
</style>
