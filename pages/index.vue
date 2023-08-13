<template>
  <div class="page client-wrapper">
    <home-navigation />

    <!-------------CAROUSEL SECTION------------->
    <div
      data-delay="4000"
      data-animation="slide"
      class="home-slider w-slider"
      data-autoplay="false"
      data-easing="ease"
      data-hide-arrows="false"
      data-disable-swipe="false"
      data-autoplay-limit="0"
      data-nav-spacing="3"
      data-duration="500"
      data-infinite="true"
    >
      <div class="mask w-slider-mask">
        <div
          v-for="banner in banners"
          :key="banner._id"
          class="slider w-slide"
          :style="{
            backgroundImage: `url(${FILE_URL}/${banner.bannerImage})`,
            backgroundSize: 'cover',
          }"
        >
          <div class="hero-cover">
            <div class="custom-container">
              <div class="hero-flex">
                <div class="hero-container">
                  <h1 class="main-heading">
                    {{ banner.bannerTitle }}
                  </h1>
                  <div class="colored-hero-text">
                    {{ banner.bannerSubtitle }}
                  </div>
                  <nuxt-link to="/about" class="hero-button w-button"
                    >READ MORE</nuxt-link
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="nav-arrow w-slider-arrow-left">
        <div class="nav-arrow-icon w-icon-slider-left"></div>
      </div>
      <div class="nav-arrow w-slider-arrow-right">
        <div class="nav-left-icon w-icon-slider-right"></div>
      </div>
      <div class="slide-nav w-slider-nav w-round"></div>
    </div>
    <!-------X-----CAROUSEL SECTION------X------>

    <!-------------WHY US------------->
    <div class="video-section">
      <div class="custom-container">
        <div class="video-flex">
          <div class="video-top-board">
            <h2 class="board-heading">
              Invest now in
              <span class="text-span">bitcoin</span> currency<br />and earn more
              later.
            </h2>
            <div class="each-board-wrapper">
              <div class="each-board-container">
                <img
                  src="https://uploads-ssl.webflow.com/64584677a42c076b5ad19e3c/6458d4d5c2dd95017d34228d_server-lock-icon%201.svg"
                  loading="lazy"
                  alt=""
                />
                <div class="board-title">Safe &amp; Secure<br /></div>
                <div>
                  Trade Live Limited prioritizes the security of its clients'
                  funds. We have implemented robust security measures, including
                  advanced encryption protocols and multi-factor authentication,
                  to safeguard your cryptocurrencies against potential threats.
                </div>
              </div>
              <div class="each-board-container">
                <img
                  src="https://uploads-ssl.webflow.com/64584677a42c076b5ad19e3c/6458d4d58291486186b7b989_crypto-exchange-icon%201.svg"
                  loading="lazy"
                  alt=""
                />
                <div class="board-title">Instant Exchange<br /></div>
                <div>
                  Instant exchange allows for immediate and real-time
                  transactions within the blockchain network. Traditional
                  financial systems often involve delays, intermediaries, and
                  settlement periods, whereas instant exchanges leverage the
                  decentralized nature of blockchain technology to enable
                  instant value transfer.
                </div>
              </div>
            </div>
          </div>
          <div class="why-us">
            <h2 class="title-header">Why Choose Us?</h2>
            <div class="line"></div>
            <div class="why-us-text">
              We understand that investors seek profitable returns on their
              investments. At Trade Live Limited, we strive to offer attractive
              interest rates to our clients, ensuring that their investments
              grow over time. Our team of experienced financial experts
              carefully analyzes market trends to make informed investment
              decisions, maximizing the potential returns for our clients.
            </div>
            <img
              src="/images/building.webp"
              loading="lazy"
              sizes="(max-width: 479px) 96vw, (max-width: 767px) 94vw, 638.9931030273438px"
              srcset="/images/building.webp 500w, /images/building.webp 639w"
              alt=""
              class="why-us-img"
            />
          </div>
        </div>
      </div>
    </div>
    <!-------X-----WHY US------X------>

    <!-------------FEATURES------------->
    <div class="get-started-section">
      <div class="custom-container">
        <h2 class="title-header">What We Offer</h2>
        <div class="line"></div>
        <div class="why-us-text">
          Trade Live Limited Offers services more than just depositing funds and
          withdrawing capital, our services provides privacy & security to your
          data, bonus incentives for your referral efforts and good customer
          support to your needs.
        </div>
        <div class="get-started-flex">
          <div
            class="each-get-started second"
            @mouseenter="second = true"
            @mouseleave="second = false"
            :class="{ active: second }"
          >
            <div class="rounded-holder">
              <img
                src="https://uploads-ssl.webflow.com/64584677a42c076b5ad19e3c/6458e105c2dd95555b351ea1_wallet.svg"
                loading="lazy"
                alt=""
                class="rounded-icon"
              />
            </div>
            <div class="board-title white">Easy Deposit</div>
            <div class="get-started-body">
              <div class="board-title white">Easy Deposit</div>
              <div class="custom-text white">
                With our multiple payment systems and an automatic scan code
                generator, you can deposit with ease in your dashboard to fund
                your account.
              </div>
            </div>
          </div>

          <div
            class="each-get-started"
            @mouseenter="first = true"
            @mouseleave="first = false"
            :class="{ active: first }"
          >
            <div class="rounded-holder">
              <img
                src="https://uploads-ssl.webflow.com/64584677a42c076b5ad19e3c/6458df162bbaac80e39a9bb8_investment.svg"
                loading="lazy"
                alt=""
                class="rounded-icon"
              />
            </div>
            <div class="board-title white">Financial Growth</div>
            <div class="get-started-body">
              <div class="board-title white">Financial Growth</div>
              <div class="custom-text white">
                Our fidelity to our client can be seen after 24 hours of your
                investment which you will see steady daily growth of your
                capital for your investment duration.
              </div>
            </div>
          </div>

          <div
            class="each-get-started"
            @mouseenter="third = true"
            @mouseleave="third = false"
            :class="{ active: third }"
            :style="{ backgroundImage: `url(/images/bit03.jpg)` }"
          >
            <div class="rounded-holder">
              <img
                src="/images/grow.svg"
                loading="lazy"
                alt=""
                class="rounded-icon"
              />
            </div>
            <div class="board-title white">Bitcoin Transaction</div>
            <div class="get-started-body">
              <div class="board-title white">Bitcoin Transaction</div>
              <div class="custom-text white">
                Successful businesses have many things in common, today we’ll
                look at the big ‘R’of recognitional advertising network may
                help.<br />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-------X-----FEATURES------X------>

    <!-------------CRYPTO------------->
    <div class="brief-services">
      <div class="custom-container">
        <!---<div class="buy-crypto-flex">
          <div class="buy-crypto-left">
            <h2 class="title-header left">{{ firstBlog.title }}</h2>
            <div class="line left"></div>
            <div
              v-if="firstBlog.content"
              class="text-custom"
              v-html="`${firstBlog.content.substring(0, 400)}..`"
            ></div>
            <nuxt-link
              :to="`/news-details/${firstBlog._id}`"
              class="hero-button w-button"
              >Read More</nuxt-link
            >
          </div>
          <div class="buy-crypto-left right">
            <div class="btcwdgt-chart" bw-theme="light"></div>
          </div>
        </div>-->
        <div
          v-for="(blog, int) in companyBlogs"
          :key="blog._id"
          class="each-service-flex"
          :class="{ reverse: int % 2 == 0 }"
        >
          <div class="each-flex-img">
            <img
              :src="`${FILE_URL}/${blog.banner}`"
              loading="lazy"
              sizes="(max-width: 479px) 96vw, (max-width: 767px) 95vw, (max-width: 991px) 46vw, (max-width: 1279px) 47vw, (max-width: 1439px) 43vw, 49vw"
              :srcset="`
                ${FILE_URL}/${blog.banner} 500w,
                ${FILE_URL}/${blog.banner}      585w
              `"
              alt=""
              class="service-img"
            />
          </div>
          <div class="each-service-content" :class="{ reverse: int % 2 == 0 }">
            <h2 class="title-header left">{{ blog.title }}</h2>
            <div class="line left"></div>
            <div
              v-if="blog.content"
              class="text-custom"
              v-html="`${blog.content.substring(0, 300)}...`"
            ></div>
            <nuxt-link
              :to="`/news-details/${blog._id}`"
              class="hero-button w-button"
              >Read More</nuxt-link
            >
          </div>
        </div>
      </div>
    </div>
    <!-------X-----CRYPTO------X------>

    <!-------------STAFFS------------->
    <div class="staffs">
      <div class="custom-container">
        <h2 class="title-header">Our Members</h2>
        <div class="line"></div>
        <div class="why-us-text">
          We are happy to present you our the Executive Staff Members of Trade
          Live Limited, the engines behind our platform's daily profits.
        </div>
        <div class="staff-flex">
          <div
            v-for="staff in staffs"
            :key="staff._id"
            class="each-staff-wrapper"
          >
            <div
              class="each-staff-img"
              :style="{ backgroundImage: `url(${FILE_URL}/${staff.image})` }"
            ></div>
            <h1 class="heading">{{ staff.name }}</h1>
            <h1 class="heading">{{ staff.position }}</h1>
            <h1 class="heading-2">
              {{ staff.quote }}
            </h1>
          </div>
        </div>
      </div>
    </div>
    <!-------X-----STAFFS------X------>

    <testimony />

    <div class="our-news">
      <div class="custom-container">
        <div>
          <h2 class="title-header our-news">Our News</h2>
          <h1 class="heading-7">
            Get the latest updates about the trends in the global market and
            explore to make profitable investment decisions.
          </h1>
          <div class="line our-news"></div>
          <div class="div-block-16">
            <div class="div-block-17" v-for="(item, int) in news" :key="int">
              <nuxt-link
                v-if="item"
                :to="`/news-details/${item._id}`"
                class="link-block w-inline-block"
                ><img
                  :src="`${FILE_URL}/${item.banner}`"
                  loading="lazy"
                  sizes="(max-width: 479px) 96vw, (max-width: 767px) 45vw, (max-width: 991px) 29vw, (max-width: 1279px) 30vw, (max-width: 1439px) 28vw, 31vw"
                  :srcset="`
                    ${FILE_URL}/${item.banner}  500w,
                    ${FILE_URL}/${item.banner}  800w,
                    ${FILE_URL}/${item.banner}       1170w
                  `"
                  alt=""
                  class="image-3"
              /></nuxt-link>
              <div class="div-block-18">
                <nuxt-link
                  v-if="item"
                  :to="`/news-details/${item._id}`"
                  class="link-block-2 w-inline-block"
                  ><h1 class="heading-8">
                    {{ item.title }}
                  </h1></nuxt-link
                >
                <div
                  v-if="item"
                  class="heading-9"
                  v-html="item.content.substring(0, 150)"
                ></div>
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
import Testimony from "../components/Testimony.vue";
export default {
  data() {
    return {
      banners: [],
      first: false,
      second: false,
      third: false,
      staffs: [],
      reviews: [],
      companyBlogs: [],

      firstBlog: "",
      twoBlogs: [],
      news: [],
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

    loadCoin() {
      if (!process.server) {
        let el = document.getElementById("bitcoin");

        if (el != undefined) {
          document.body.removeChild(el);
        }

        const script = document.createElement("script");
        script.type = "text/javascript";
        script.src = "/script/bitcoin.js";
        script.async = true;
        script.id = "bitcoin";
        const app = document.querySelector("#footer");
        if (app) {
          app.appendChild(script);
        } else {
          console.error("Could not find app node to append script element");
        }
      }
    },

    getTwoBlogs(data) {
      const blogs = [];
      for (let i = 0; i < 3; i++) {
        blogs.push(data[i]);
      }

      return blogs;
    },

    getCompanyBlogs(data) {
      const blogArr = [];
      data.forEach((el) => {
        if (el.category != "Crypto") {
          blogArr.push(el);
        }
      });

      return blogArr;
    },

    getNews(data) {
      const blogs = [];
      data.forEach((el) => {
        if (el.category == "Crypto") {
          blogs.push(el);
        }
      });

      return blogs;
    },

    async getStaffs() {
      try {
        const result = await this.$axios.get(`/staffs`);
        this.staffs = result.data.data;
      } catch (err) {
        console.log(err.response.data.message);
      }
    },

    async getBlogs() {
      try {
        const result = await this.$axios.get("/blog");
        this.companyBlogs = this.getCompanyBlogs(result.data.data);
        this.firstBlog = result.data.data[0];
        this.secondBlog = result.data.data[1];
        this.twoBlogs = this.getTwoBlogs(result.data.data);
        this.news = this.getNews(result.data.data);
        this.blogs = result.data.data;
      } catch (err) {
        console.log(err.response);
      }
    },

    async getBanner() {
      try {
        const result = await this.$axios.get(`/banner/?bannerCategory=Home`);
        this.banners = result.data.data;
        this.loadScript();
      } catch (err) {
        console.log(err);
      }
    },

    async getCompany() {
      try {
        const result = await this.$axios.get("/company");
        this.company = await result.data.data;
        this.time = this.company.dayStarted;
        this.startClock();
      } catch (err) {
        console.log(err.response.data);
      }
    },

    async getStaffs() {
      try {
        const result = await this.$axios.get(`/staffs`);
        this.staffs = result.data.data;
      } catch (err) {
        console.log(err.response.data.message);
      }
    },

    async getPartners() {
      try {
        const result = await this.$axios.get(`/partners`);
        this.partners = result.data.data;
      } catch (err) {
        console.log(err.response.data.message);
      }
    },

    async getEvents() {
      try {
        const result = await this.$axios.get(`/events`);
        this.events = result.data.data;
      } catch (err) {
        console.log(err.response.data.message);
      }
    },
  },
  mounted() {
    this.getBanner();
    this.getBlogs();
    this.loadCoin();
    this.getStaffs();
    // this.getEvents();
    // this.getPartners();
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
.each-get-started .get-started-body {
  transition: all 0.4s;
}

.each-get-started.active .get-started-body {
  opacity: 1;
  z-index: 2;
}

.div-block-5 .div-block-6 {
  width: 100%;
}

.image.review {
  object-fit: cover;
}

.mask.w-slider-mask {
  min-height: 70vh;
}
</style>
