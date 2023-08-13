<template>
  <!-------------REVIEWS------------->
  <div class="company-skills-and-client-testimonial">
    <div class="custom-container">
      <div class="staff-skills">
        <div class="div-block-2">
          <h2 class="title-header company-skilla">Company's Progress</h2>
          <h1 class="heading-3">
            Our long years of success has also been based on our distribution of
            labour across our work force. While our overall goal per year has
            been splitted into units we are hoping to reach 100% completion of
            our yearly goal, yet our current stats is below.
          </h1>
          <div class="div-block-4">
            <div class="line company-skills"></div>
          </div>
          <div class="div-block-5">
            <div class="div-block-6">
              <div class="div-block-7">
                <h1 class="heading-4">
                  <strong class="bold-text">Crypto Mining</strong>
                </h1>
                <h1 class="heading-4">
                  <strong class="bold-text-2">95%</strong>
                </h1>
              </div>
              <div class="div-block-8">
                <div class="div-block-9"></div>
              </div>
            </div>
            <div class="div-block-6">
              <div class="div-block-7">
                <h1 class="heading-4">
                  <strong class="bold-text">Cloud Hosting</strong>
                </h1>
                <h1 class="heading-4">
                  <strong class="bold-text-2">78%</strong>
                </h1>
              </div>
              <div class="div-block-8">
                <div class="div-block-9 _2"></div>
              </div>
            </div>
            <div class="div-block-6">
              <div class="div-block-7">
                <h1 class="heading-4">
                  <strong class="bold-text">Secured Exchange</strong>
                </h1>
                <h1 class="heading-4">
                  <strong class="bold-text-2">60%</strong>
                </h1>
              </div>
              <div class="div-block-8">
                <div class="div-block-9 _3"></div>
              </div>
            </div>
          </div>
        </div>
        <div class="div-block-3">
          <h2 class="title-header company-skillb">Client Testimonials</h2>
          <div class="div-block-4 _2">
            <div class="line company-skills"></div>
          </div>
          <div
            data-delay="4000"
            data-animation="slide"
            class="slider-2 w-slider"
            data-autoplay="false"
            data-easing="ease"
            data-hide-arrows="false"
            data-disable-swipe="false"
            data-autoplay-limit="0"
            data-nav-spacing="3"
            data-duration="500"
            data-infinite="true"
          >
            <div class="w-slider-mask">
              <div
                v-for="review in reviews"
                :key="review._id"
                class="slide w-slide"
              >
                <div class="div-block-10">
                  <div class="div-block-11">
                    <h1 class="heading-5">
                      {{ review.comment }}
                    </h1>
                  </div>
                  <div class="div-block-12">
                    <div class="div-block-13">
                      <img
                        :src="`${FILE_URL}/${review.profilePicture}`"
                        loading="lazy"
                        alt=""
                        class="image review"
                      />
                    </div>
                    <div class="div-block-15">
                      <h1 class="heading-6">
                        {{ review.username }}
                        <span class="text-span-2">Cryptobit Investor</span>
                      </h1>
                      <div class="div-block-14">
                        <span>{{ review.rating }}</span>
                        <img
                          src="https://uploads-ssl.webflow.com/64584677a42c076b5ad19e3c/645c12b2516edcf87d2a2876_star-symbol-icon.svg"
                          loading="lazy"
                          alt=""
                          class="image-2"
                        />
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="w-slider-arrow-left"></div>
            <div class="w-slider-arrow-right"></div>
            <div class="w-slider-nav w-round w-num"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-------X-----REVIEWS------X------>
</template>

<script>
export default {
  data() {
    return {
      reviews: [],
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

    async getReviews() {
      try {
        const result = await this.$axios.get("/review/?commented=true");
        this.reviews = await result.data?.data;
      } catch (err) {
        console.log(err);
      }
    },
  },
  mounted() {
    this.getReviews();
  },
  computed: {
    FILE_URL() {
      return this.$store.state.fileURL;
    },
  },
};
</script>

<style>
.slider-2.w-slider {
  height: auto;
}
</style>
