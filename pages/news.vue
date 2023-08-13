<template>
  <div class="blog client-wrapper">
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
            <h1 class="heading-24">Blog Posts</h1>
          </div>
        </div>
      </div>
      <div class="div-block-29"></div>
    </div>

    <div class="blog-section3">
      <div class="custom-container">
        <div class="div-block-49">
          <div class="div-block-50">
            <div v-for="blog in blogs" :key="blog._id" class="div-block-58">
              <img
                :src="`${FILE_URL}/${blog.banner}`"
                loading="lazy"
                alt=""
                class="image-7"
              />
              <div>
                <nuxt-link
                  :to="`/news-details/${blog._id}`"
                  class="heading-42 title"
                  >{{ blog.title }}</nuxt-link
                >
                <div
                  class="heading-43"
                  v-html="`${blog.content.substring(0, 300)}...`"
                ></div>
              </div>
            </div>
            <!-- <span class="link-block-11 w-inline-block"
              ><h1 class="heading-44">Next</h1>
              <div class="div-block-54">
                <img
                  src="https://uploads-ssl.webflow.com/64584677a42c076b5ad19e3c/6461c89c4bc9d89c2d007be6_right-arrow-next-svgrepo-com%201%20(1).svg"
                  loading="lazy"
                  alt=""
                  class="image-9"
                /></div
            ></span> -->
          </div>
          <aside-news />
        </div>
      </div>
    </div>
    <home-footer />
  </div>
</template>

<script>
import AsideNews from "../components/AsideNews.vue";
import HomeFooter from "../components/HomeFooter.vue";
import HomeNavigation from "../components/HomeNavigation.vue";
export default {
  data() {
    return {
      blogs: [],
      banner: "",
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
        const result = await this.$axios.get(`/banner/?bannerCategory=Blog`);
        this.banner = result.data.data[0];
      } catch (err) {
        console.log(err);
      }
    },

    async getBlogs() {
      try {
        const result = await this.$axios.get("/blog");
        this.blogs = result.data.data;
      } catch (err) {
        console.log(err.response);
      }
    },
  },
  mounted() {
    this.loadScript();
    this.getBlogs();
    this.getBanner();
  },
  computed: {
    FILE_URL() {
      return this.$store.state.fileURL;
    },
  },
  components: { HomeNavigation, HomeFooter, AsideNews },
};
</script>

<style>
a.heading-42.title {
  margin: 30px 0;
}
</style>
