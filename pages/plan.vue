<template>
  <div class="faq plan client-wrapper">
    <home-navigation />
    <div
      class="about-us-section faq"
      :style="{ backgroundImage: `url(${FILE_URL}/${banner.bannerImage})` }"
    >
      <div class="custom-container">
        <div class="hero-section">
          <h1 class="heading-21 faq">{{ banner.bannerTitle }}</h1>
          <!-- <h1 class="heading-22 faq">{{ banner.bannerSubtitle }}</h1> -->
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
            <h1 class="heading-24">Plan</h1>
          </div>
        </div>
      </div>
      <div class="div-block-29"></div>
    </div>

    <div class="plan-section">
      <div class="custom-container">
        <div class="plan-card-holder">
          <div v-for="plan in plans" :key="plan._id" class="plan-each-card">
            <div class="plan-header-holder">
              <h1 class="plan-card-header">{{ plan.planName }}</h1>
            </div>
            <div class="percent-border-holder">
              <div class="percent-text front">%</div>
              <h1 class="percent-header">{{ plan.planPercentage }}</h1>
              <div class="percent-text back">Daily</div>
            </div>
            <div class="plan-option-holder">
              <div class="each-plan-option">
                <img
                  src="https://uploads-ssl.webflow.com/64584677a42c076b5ad19e3c/64680eaba638d283b179f5a3_check-mark-circle-icon%202.svg"
                  loading="lazy"
                  alt=""
                  class="image-11"
                />
                <div class="odd-header">MiniMum Investment:</div>
                <div class="percent-text">
                  ${{ formatMoney(plan.planMinimum) }} USD
                </div>
              </div>
              <div class="each-plan-option">
                <img
                  src="https://uploads-ssl.webflow.com/64584677a42c076b5ad19e3c/64680eaba638d283b179f5a3_check-mark-circle-icon%202.svg"
                  loading="lazy"
                  alt=""
                  class="image-11"
                />
                <div class="odd-header">Maximum Investment:</div>
                <div v-if="plan.planMaximum > 0" class="percent-text">
                  ${{ formatMoney(plan.planMaximum) }} USD
                </div>
                <div v-else class="percent-text">UNLIMITED</div>
              </div>
              <div class="each-plan-option">
                <img
                  src="https://uploads-ssl.webflow.com/64584677a42c076b5ad19e3c/64680eaba638d283b179f5a3_check-mark-circle-icon%202.svg"
                  loading="lazy"
                  alt=""
                  class="image-11"
                />
                <div class="odd-header">Investment Duration:</div>
                <div class="percent-text">{{ plan.planDuration }} Days.</div>
              </div>
              <div class="each-plan-option">
                <img
                  src="https://uploads-ssl.webflow.com/64584677a42c076b5ad19e3c/64680eaba638d283b179f5a3_check-mark-circle-icon%202.svg"
                  loading="lazy"
                  alt=""
                  class="image-11"
                />
                <div class="odd-header">Referral Commission</div>
                <div class="percent-text">{{ plan.referralCommission }}%</div>
              </div>
            </div>
            <div class="card-button-holder">
              <nuxt-link to="/login" class="w-button plann"
                >Invest Now</nuxt-link
              >
            </div>
          </div>
        </div>
      </div>
    </div>
    <testimony />
    <home-footer />
  </div>
</template>

<script>
import HomeFooter from "../components/HomeFooter.vue";
import HomeNavigation from "../components/HomeNavigation.vue";
import Testimony from "../components/Testimony.vue";
export default {
  data() {
    return {
      plans: [],
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

    formatMoney(amount) {
      if (amount == "" || amount == null || amount == undefined) {
        return "0.00";
      } else {
        return amount.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
      }
    },

    async getBanner() {
      try {
        const result = await this.$axios.get(`/banner/?bannerCategory=Plan`);
        this.banner = result.data.data[0];
      } catch (err) {
        console.log(err);
      }
    },

    async getPlans() {
      try {
        const result = await this.$axios.get("/plans");
        this.plans = result.data.data;
      } catch (err) {
        console.log(err.response);
      }
    },
  },
  mounted() {
    this.loadScript();
    this.getPlans();
    this.getBanner();
  },
  computed: {
    FILE_URL() {
      return this.$store.state.fileURL;
    },
  },
  components: { HomeNavigation, HomeFooter, Testimony },
};
</script>

<style>
.w-button.plann {
  background-color: #ffb426;
  border-radius: 5px;
}
</style>
