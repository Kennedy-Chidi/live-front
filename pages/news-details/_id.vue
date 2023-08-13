<template>
  <div class="blog full-blog">
    <home-navigation />

    <div
      class="about-us-section faq"
      :style="{ backgroundImage: `url(${FILE_URL}/${blog.banner})` }"
    >
      <div class="custom-container">
        <div class="hero-section">
          <h1 class="heading-21 faq">{{ blog.title }}</h1>
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
            <h1 class="heading-24">Blog Details</h1>
          </div>
        </div>
      </div>
      <div class="div-block-29"></div>
    </div>

    <div class="blog-section3">
      <div class="custom-container">
        <div class="div-block-49">
          <div class="div-block-50">
            <img
              :src="`${FILE_URL}/${blog.banner}`"
              loading="lazy"
              alt=""
              class="image-7"
            />
            <div>
              <h1 class="heading-42">{{ blog.title }}</h1>
              <div class="heading-43" v-html="blog.content"></div>
            </div>
          </div>
          <aside-news />
        </div>
      </div>
    </div>
    <home-footer />
  </div>
</template>

<script>
import AsideNews from "../../components/AsideNews.vue";
import HomeFooter from "../../components/HomeFooter.vue";
import HomeNavigation from "../../components/HomeNavigation.vue";
export default {
  data() {
    return {
      blog: "",
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

    async getBlog(id) {
      try {
        const result = await this.$axios.get(`/blog/${id}`);
        this.blog = result.data.data;
        this.loadScript();
      } catch (err) {
        console.log(err.response.data);
      }
    },
  },
  mounted() {
    this.getBlog(this.$route.params.id);
  },
  computed: {
    FILE_URL() {
      return this.$store.state.fileURL;
    },
  },
  components: { HomeFooter, HomeNavigation, AsideNews },
};
</script>

<style></style>
