<template>
  <div class="page public">
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
      <div class="landing-flex full person">
        <div class="custom-container"></div>
      </div>
    </div>
    <div class="custom-container">
      <div class="blog-body full person">
        <div class="main-blog-header">
          <div class="person-bg-holder"><div class="person-bg"></div></div>
          <h1 class="main-title">AMANDA KINGSLEY</h1>
          <div class="person-country">
            <img
              src="https://uploads-ssl.webflow.com/6458b19446eea345a074cdaf/645c2e6de2cee60513a66c41_nz.svg"
              loading="lazy"
              alt=""
              class="person-flag"
            /><a href="#" class="person-country-name">Australia</a>
          </div>
          <div class="each-online-stat person">
            <div class="online-label-holder">
              <h4 class="online-stat-title">Yearly Progress</h4>
              <h4 class="online-stat-title percent">70%</h4>
            </div>
            <div class="online-bar-body person">
              <div class="online-active-bar"></div>
            </div>
          </div>
          <div class="main-intro-text">
            INVESTOR OF THE WEEK/ JULY 20 - 27, 2023 / PERSONAL GROWTH
          </div>
        </div>
        <div class="blog-flex">
          <div class="main-blog-body person">
            <div class="main-content">
              I’m baby direct trade cliche cloud bread hammock kinfolk deep v.
              Irony PBR&amp;B schlitz, bespoke jianbing post-ironic enamel pin
              lyft copper mug narwhal before they sold out distillery roof party
              8-bit cardigan.<br /><br />Bushwick post-ironic af fixie,
              wayfarers kombucha
              <a
                href="https://level.uicore.co/layouts/2021/07/20/10-simple-practices-that-will-help-you-get-1-better-every-day/#"
                >direct trade</a
              >
              air plant meditation palo santo asymmetrical salvia blue bottle. 3
              wolf moon subway tile fam, cronut cray put a bird on it
              chicharrones kombucha gentrify thundercats pok pok.<br /><br />Whatever
              wolf leggings yuccie +1 90’s, austin ennui listicle hashtag
              church-key master cleanse hexagon mlkshk kitsch. Dreamcatcher ugh
              jianbing palo santo blog hashtag brunch. Hoodie taxidermy prism
              venmo blue bottle next level
              <a
                href="https://level.uicore.co/layouts/2021/07/20/10-simple-practices-that-will-help-you-get-1-better-every-day/#"
                >neutra vaporware</a
              >
              typewriter af plaid retro freegan.
            </div>
          </div>
        </div>
      </div>
    </div>
    <home-footer />
  </div>
</template>

<script>
import HomeFooter from "../../components/HomeFooter.vue";
import HomeNavigation from "../../components/HomeNavigation.vue";
export default {
  components: { HomeNavigation, HomeFooter },
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
  },
  mounted() {
    this.loadScript();
  },
};
</script>

<style></style>
