<template>
  <div class="contact client-wrapper">
    <home-navigation />
    <div class="contact-section">
      <iframe
        src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d2711.832597284578!2d8.517534415615778!3d47.180714079158705!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x479aaa5aa1146fcf%3A0x10a54b35e8298daf!2sAhornstrasse%206%2C%206300%20Zug%2C%20Switzerland!5e0!3m2!1sen!2sng!4v1685354700465!5m2!1sen!2sng"
        width="100%"
        height="100%"
        style="border: 0"
        allowfullscreen=""
        loading="lazy"
        referrerpolicy="no-referrer-when-downgrade"
      ></iframe>
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
            <h1 class="heading-24">Contact</h1>
          </div>
        </div>
      </div>
      <div class="div-block-29"></div>
    </div>
    <div class="contact-section2">
      <div class="custom-container">
        <div class="div-about4 contact2">
          <h2 class="title-header about-us4 contact2">Get In Touch</h2>
          <div class="div-block-44">
            <div class="form-block-2 w-form">
              <div class="form-2">
                <input
                  type="text"
                  class="text-field-3 w-input"
                  maxlength="256"
                  placeholder="Subject"
                  required=""
                  v-model="name"
                />
                <input
                  type="email"
                  class="text-field4 w-input"
                  maxlength="256"
                  placeholder="example@gmai.com"
                  required=""
                  v-model="email"
                />
                <textarea
                  placeholder="Write Message Here..."
                  maxlength="5000"
                  class="textarea w-input"
                  v-model="content"
                ></textarea>

                <div
                  v-if="showResponse"
                  class="feedback"
                  :class="{ error: isError }"
                >
                  {{ response }}
                </div>
                <input
                  v-if="onRequest"
                  type="submit"
                  value="Processing..."
                  class="submit-button-2 w-button"
                />
                <input
                  v-else
                  type="submit"
                  value="Send Message"
                  @click="sendMessage"
                  class="submit-button-2 w-button"
                />
              </div>
            </div>
            <div class="div-block-45">
              <h1 class="heading-34">
                Feel free to reach us personal and get quick response to all
                your your enquiries through our contact media below.
              </h1>
              <div v-if="phone" class="div-block-24 contact2">
                <h1 class="heading-16 contact2">
                  Phone <span class="text-span-3">:</span>
                </h1>
                <h1 class="heading-17 contact2">{{ phone.text }}</h1>
              </div>
              <div v-if="company" class="div-block-24 contact2">
                <h1 class="heading-16 contact2">
                  <strong>Email</strong> <span class="text-span-3">:</span>
                </h1>
                <h1 class="heading-17 contact2">{{ company.systemEmail }}</h1>
              </div>
              <div class="div-block-24 contact2">
                <h1 class="heading-16 contact2">
                  <strong>Working</strong>
                  <span class="text-span-3">:</span>
                </h1>
                <h1 class="heading-17 contact2">Mon - Sun: 8:00 - 17:30</h1>
              </div>
              <div v-if="address" class="div-block-24 contact2 _4">
                <h1 class="heading-16 contact2">
                  <strong>Address :</strong>
                </h1>
                <h1 class="heading-17 contact2">
                  {{ address.text }}
                </h1>
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
      company: "",
      address: "",
      phone: "",

      content: "",
      name: "",
      email: "",

      response: "",
      isError: false,
      showResponse: false,
      onRequest: false,
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

    clearInputs() {
      this.email = "";
      this.name = "";
      this.content = "";
    },

    callResponse(msg, state) {
      this.response = msg;
      this.isError = state;
      this.showResponse = true;
      this.onRequest = false;
      setTimeout(() => {
        this.showResponse = false;
      }, 6000);
    },

    async getCompany() {
      try {
        const result = await this.$axios.get(`/company`);
        this.company = result.data.data[0];
        this.media = this.company.media;
        this.loadScript();
      } catch (err) {
        console.log(err);
      }
    },

    async sendMessage() {
      this.onRequest = true;
      if (this.name == "" || this.name.length < 2) {
        this.callResponse("Please write a valid name.", true);
        return;
      }
      if (
        this.email == "" ||
        !this.email ||
        !/^\S+@\S+\.\S+$/.test(this.email)
      ) {
        this.callResponse("Please provide a valid email.", true);
        return;
      }
      if (this.content.trim() == "" || this.content.length < 30) {
        this.callResponse(
          "Sorry content must be at least 30 characters long.",
          true
        );
        return;
      }

      const form = {
        name: this.name,
        email: this.email,
        content: this.content,
      };

      try {
        await this.$axios.post(`/emails/send-message`, form);
        this.callResponse("Message sent successfully", false);
        this.clearInputs();
      } catch (err) {
        this.callResponse(err.response.data.message);
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
    this.getCompany();
  },
  components: { HomeFooter, HomeNavigation },
};
</script>

<style>
.feedback {
  width: 100%;
  font-weight: bold;
}

.feedback.error {
  color: red;
}
</style>
