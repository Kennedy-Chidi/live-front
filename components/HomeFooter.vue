<template>
  <div class="footer1" id="footer">
    <div class="custom-container">
      <div class="div-block-25">
        <div class="div-block-20">
          <div class="div-block-19">
            <h1 class="heading-10">QUICK LINKS</h1>
            <div class="div-block-21">
              <div class="link-block-3 w-inline-block">
                <nuxt-link to="/" class="heading-11">Home</nuxt-link>
                <nuxt-link to="/about" class="heading-11">About Us</nuxt-link>
                <nuxt-link to="/plan" class="heading-11">Plans</nuxt-link>
                <nuxt-link to="/contact" class="heading-11">Contact</nuxt-link>
                <nuxt-link to="/news" class="heading-11">Blog</nuxt-link>
              </div>
              <div class="link-block-3 w-inline-block">
                <nuxt-link to="/signup" class="heading-11">Sign up</nuxt-link>
                <nuxt-link to="/login" class="heading-11">Login</nuxt-link>
                <nuxt-link to="/terms-conditions" class="heading-11"
                  >Terms & Conditions</nuxt-link
                >
              </div>
            </div>
          </div>
          <div class="div-block-22">
            <h1 class="heading-12">NEWSLETTER SIGNUP</h1>
            <h1 class="heading-13">
              By subscribing to our mailing list you will always be update with
              the latest news from us.
            </h1>
            <div class="form-block w-form">
              <form
                id="email-form"
                name="email-form"
                data-name="Email Form"
                method="get"
                class="form"
              >
                <input
                  type="email"
                  class="text-field w-input"
                  maxlength="256"
                  name="email"
                  data-name="Email"
                  placeholder="Email"
                  id="email"
                  required=""
                /><input
                  type="submit"
                  value="Sign Up"
                  data-wait="Please wait..."
                  class="submit-button w-button"
                />
              </form>
            </div>
            <h1 class="heading-14">We don&#x27;t spam.</h1>
          </div>
          <div class="div-block-23">
            <h1 class="heading-15">GET IN TOUCH</h1>
            <div v-if="phone" class="div-block-24">
              <h1 class="heading-16">
                Phone <span class="text-span-3">:</span>
              </h1>
              <h1 class="heading-17">{{ phone.text }}</h1>
            </div>
            <div v-if="company" class="div-block-24 b">
              <h1 class="heading-16">
                Email <span class="text-span-3">:</span>
              </h1>
              <h1 class="heading-17">{{ company.systemEmail }}</h1>
            </div>
            <h1 v-if="address" class="heading-18">{{ address.text }}</h1>
            <!-- <a href="#" class="link-block-4 w-inline-block"
              ><h1 class="heading-19">Open in Google Map</h1></a
            > -->
          </div>
        </div>
      </div>
    </div>
    <div class="footer-line"></div>
    <h1 v-if="company" class="heading-20">
      {{ company.companyName }} © {{ new Date().getFullYear() }} Copyrights. All
      rights reserved.
    </h1>
  </div>
</template>

<script>
export default {
  data() {
    return {
      company: "",
      address: "",
      phone: "",
    };
  },
  methods: {
    setFileURL() {
      this.$store.commit("SET_URL", this.$config.FILE_URL);
    },

    loadScript() {
      if (!process.server) {
        let el1 = document.getElementById("translator");

        if (el1 != undefined) {
          document.body.removeChild(el1);
        }

        const scriptTranslate = document.createElement("script");
        scriptTranslate.type = "text/javascript";
        scriptTranslate.src =
          "https://translate.yandex.net/website-widget/v1/widget.js?widgetId=ytWidget&pageLang=en&widgetTheme=light&autoMode=false";
        scriptTranslate.async = true;
        scriptTranslate.id = "translator";
        const app = document.querySelector("#footer");
        if (app) {
          app.appendChild(scriptTranslate);
        } else {
          console.error("Could not find app node to append script element");
        }
      }
    },

    async getCompany() {
      try {
        const result = await this.$axios.get("/company");
        this.company = await result.data.data;
        this.address = result.data.data.media[0];
        this.phone = result.data.data.media[2];
      } catch (err) {
        console.log(err.response.data);
      }
    },
  },
  mounted() {
    this.loadScript();
    this.setFileURL();
    this.getCompany();
  },
};
</script>

<style>
.custom-container.footer {
  background: #00040f;
}

.w-inline-block a {
  display: block;
  color: white;
  font-weight: 300;
}
</style>
