<template>
  <div class="create-account client-wrapper">
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

    <div class="about-us-section2 create-account">
      <div class="custom-container">
        <div>
          <div class="div-block-27 faq">
            <div class="div-block-28">
              <img
                src="https://uploads-ssl.webflow.com/64584677a42c076b5ad19e3c/6460a0e746818cacc5ca3e96_home-icon-silhouette-svgrepo-com%201.svg"
                loading="lazy"
                alt=""
                class="image-4"
              />
            </div>
            <a href="#" class="link-block-5 w-inline-block"
              ><h1 class="heading-23">Home</h1>
              <img
                src="https://uploads-ssl.webflow.com/64584677a42c076b5ad19e3c/6460a0eddea363a6792c4285_left-arrow-next-svgrepo-com%201.svg"
                loading="lazy"
                alt=""
                class="image-5"
            /></a>
            <h1 class="heading-24">Create an account</h1>
          </div>
        </div>
      </div>
      <div class="div-block-29"></div>
    </div>

    <div class="login-section3 create-account">
      <div class="custom-container">
        <div class="div-block-48">
          <div class="form-block-3 w-form">
            <div class="form-3">
              <div class="form-input">
                <label for="" class="firstName"
                  >First name must be at least 2 characters</label
                >
                <input
                  type="text"
                  class="text-field-4 w-input"
                  maxlength="256"
                  v-model="firstName"
                  placeholder="Enter First Name"
                  @blur="checkErrorInputs('firstName', firstName)"
                />
              </div>
              <div class="form-input">
                <label for="" class="lastName"
                  >Last name must be at least 2 characters</label
                >
                <input
                  type="text"
                  class="text-field-4 w-input"
                  maxlength="256"
                  v-model="lastName"
                  placeholder="Enter Last Name"
                  @blur="checkErrorInputs('lastName', lastName)"
                />
              </div>
              <div class="form-input">
                <label for="" class="username"
                  >Username must be a word of at least 5 characters long</label
                >
                <input
                  type="text"
                  class="text-field-4 w-input"
                  maxlength="256"
                  v-model="username"
                  placeholder="Enter Username"
                  @blur="checkErrorInputs('username', username)"
                />
              </div>
              <div class="form-input">
                <label for="" class="email">Please enter a valid email</label>
                <input
                  type="email"
                  class="text-field-5 w-input"
                  maxlength="256"
                  name="email"
                  data-name="Email 4"
                  placeholder="Enter Email"
                  v-model="email"
                  @blur="checkErrorInputs('email', email)"
                />
              </div>
              <div class="form-input">
                <label for="" class="phoneNumber"
                  >Please enter a valid phone number</label
                >
                <input
                  type="tel"
                  class="text-field-5 w-input"
                  maxlength="256"
                  name="phone"
                  placeholder="Enter Phone Number"
                  v-model="phoneNumber"
                  @blur="checkErrorInputs('phoneNumber', phoneNumber)"
                />
              </div>
              <div class="form-input">
                <label for="" class="password"
                  >Password must be at least 6 characters long</label
                >
                <input
                  type="password"
                  class="text-field-5 w-input"
                  maxlength="256"
                  name="password"
                  placeholder="Enter Password"
                  v-model="password"
                  @blur="checkErrorInputs('password', password)"
                />
              </div>
              <div class="form-input">
                <label for="" class="cPassword">Password do not match</label>
                <input
                  type="password"
                  class="text-field-5 w-input"
                  maxlength="256"
                  name="password"
                  data-name="Confirm Password"
                  placeholder="Password"
                  v-model="cPassword"
                  @keypress.enter="processUserData"
                  @blur="checkErrorInputs('cPassword', cPassword)"
                />
              </div>

              <div class="div-block-47">
                <div
                  class="div-block-46"
                  @click="isChecked = !isChecked"
                  :class="{ active: isChecked }"
                >
                  <div class="dot"></div>
                </div>
                <span class="link-block-7 w-inline-block"
                  ><h1 class="heading-35">
                    By signing in you have agreed to our
                    <nuxt-link to="/terms-conditions" class="terms"
                      >Terms and Conditions.</nuxt-link
                    >
                  </h1></span
                >
              </div>
              <div v-if="showResponse">
                {{ response }}
              </div>

              <input
                v-if="onRequest"
                type="button"
                value="Processing..."
                class="submit-button-3 w-button stop"
              />
              <input
                v-else
                type="button"
                value="Submit"
                @click="processUserData"
                class="submit-button-3 w-button"
              />
              <h1 class="heading-36">Already have an account?</h1>
              <nuxt-link to="/login" class="link-block-8 b w-inline-block"
                ><h1 class="heading-36">Sign in</h1></nuxt-link
              >
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
      response: "",
      isError: false,
      showResponse: false,
      onRequest: false,
      countryFlag:
        "https://uploads-ssl.webflow.com/6458b19446eea345a074cdaf/645c2c8b29453fbe1844d43f_flag.svg",

      documents: ["Drivers Licence", "National ID", "International Passport"],

      firstName: "",
      lastName: "",
      username: "",
      email: "",
      phoneNumber: "",
      country: "Select Country",
      documentName: "Select Document",
      documentFile: "",
      profilePicture: "",
      avatar: "",

      passport: "",
      password: "",
      cPassword: "",
      isChecked: false,

      referral: "",

      showCountryList: false,
      showDocumentList: false,

      firstNameError: false,
      lastNameError: false,
      usernameError: false,
      emailError: false,
      phoneNumberError: false,
      countryError: false,
      documentError: false,
      passportError: false,
      passwordError: false,
      cPasswordError: false,

      signup: "",
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

    checkErrorInputs(input, data) {
      if (input == "firstName") {
        if (
          data == "" ||
          !data ||
          data.length < 2 ||
          !/^[a-zA-Z0-9]+$/.test(data)
        ) {
          const parent = this.$el.querySelector(".firstName");
          parent.classList.add("error");
          this.isError = false;
          this.firstNameError = true;
          this.onRequest = false;
          return;
        } else {
          const parent = this.$el.querySelector(".firstName");
          parent.classList.remove("error");
          this.isError = true;
          this.firstNameError = false;
        }
      } else if (input == "lastName") {
        if (
          data == "" ||
          !data ||
          data.length < 2 ||
          !/^[a-zA-Z0-9]+$/.test(data)
        ) {
          const parent = this.$el.querySelector(".lastName");
          parent.classList.add("error");
          this.isError = false;
          this.lastNameError = true;
          this.onRequest = false;
          return;
        } else {
          const parent = this.$el.querySelector(".lastName");
          parent.classList.remove("error");
          this.isError = true;
          this.lastNameError = false;
        }
      } else if (input == "username") {
        if (!data || data.length < 2 || !/^\w+$/.test(data)) {
          const parent = this.$el.querySelector(".username");
          parent.classList.add("error");
          this.isError = false;
          this.usernameError = true;
          this.onRequest = false;
          return;
        } else {
          const parent = this.$el.querySelector(".username");
          parent.classList.remove("error");
          this.isError = true;
          this.usernameError = false;
        }
      } else if (input == "phoneNumber") {
        if (data == "" || !data || !/^[0-9+]+$/.test(data)) {
          const parent = this.$el.querySelector(".phoneNumber");
          parent.classList.add("error");
          this.isError = false;
          this.phoneNumberError = true;
          this.onRequest = false;
          return;
        } else {
          const parent = this.$el.querySelector(".phoneNumber");
          parent.classList.remove("error");
          this.isError = true;
          this.phoneNumberError = false;
        }
      } else if (input == "email") {
        if (data == "" || !data || !/^\S+@\S+\.\S+$/.test(data)) {
          const parent = this.$el.querySelector(".email");
          parent.classList.add("error");
          this.isError = false;
          this.emailError = true;
          this.onRequest = false;
          return;
        } else {
          const parent = this.$el.querySelector(".email");
          parent.classList.remove("error");
          this.isError = true;
          this.emailError = false;
        }
      } else if (input == "password") {
        if (data == "" || !data || data.length < 6) {
          const parent = this.$el.querySelector(".password");
          parent.classList.add("error");
          this.isError = true;
          this.passwordError = true;
          this.onRequest = false;
          return false;
        } else {
          const parent = this.$el.querySelector(".password");
          parent.classList.remove("error");
          this.isError = true;
          this.passwordError = false;
        }
      } else if (input == "cPassword") {
        if (data != this.password || data == "") {
          const parent = this.$el.querySelector(".cPassword");
          parent.classList.add("error");
          this.isError = false;
          this.cPasswordError = true;
          this.onRequest = false;
          return;
        } else {
          const parent = this.$el.querySelector(".cPassword");
          parent.classList.remove("error");
          this.isError = true;
          this.cPasswordError = false;
        }
      }
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

    clearInputs() {
      this.firstName = "";
      (this.lastName = ""), (this.username = "");
      this.phoneNumber = "";
      this.email = "";
      this.password = "";
      this.cPassword = "";
      this.isChecked = false;
    },

    selectDocumentFile(e) {
      this.documentFile = e.target.files[0];
    },

    setProfile(e) {
      const [file] = passport.files;
      this.profilePicture = file;
      this.avatar = URL.createObjectURL(file);
    },

    setArray() {
      this.checkArray = [
        { name: "firstName", data: this.firstName },
        { name: "lastName", data: this.lastName },
        { name: "username", data: this.username },
        { name: "email", data: this.email },
        { name: "phoneNumber", data: this.phoneNumber },
        { name: "password", data: this.password },
        { name: "cPassword", data: this.cPassword },
      ];
    },

    selectCountry(data) {
      this.country = data.country;
      this.countryFlag = data.flagUrl;
      this.showCountryList = false;
    },

    selectDocumentName(data) {
      this.documentName = data;
      this.showDocumentList = false;
    },

    async getBanner() {
      try {
        const result = await this.$axios.get(`/banner/?bannerCategory=Signup`);
        this.banner = result.data.data[0];
      } catch (err) {
        console.log(err);
      }
    },

    async getSignupSettings() {
      try {
        const result = await this.$axios.post("/signup");
        this.signup = result.data.data;
        this.loadScript();
      } catch (err) {
        this.callResponse(err.response.data.message, true);
      }
    },

    async processUserData() {
      this.onRequest = true;
      this.setArray();
      this.checkArray.forEach((el) => {
        this.checkErrorInputs(el.name, el.data);
      });
      if (!this.isError) {
        return;
      }
      if (!this.isChecked) {
        this.onRequest = false;
        this.callResponse(
          "Please read and accept the terms and conditions to continue",
          true
        );
        return;
      }

      const form = new FormData();
      form.append("firstName", this.firstName);
      form.append("lastName", this.lastName);
      form.append("username", this.username);
      form.append("email", this.email);
      form.append("phoneNumber", this.phoneNumber);
      form.append("documentName", this.documentName);
      form.append("documentFile", this.documentFile);
      form.append("profilePicture", this.profilePicture);
      form.append("country", this.country);
      form.append("countryFlag", this.countryFlag);
      form.append("regDate", new Date().getTime());
      form.append("referredBy", this.referral);
      form.append("totalAmount", 0);
      form.append("password", this.password);
      form.append("cPassword", this.cPassword);

      try {
        const result = await this.$axios.post("/users/signup", form);
        this.onRequest = false;
        const msg = result.data.message;
        this.callResponse(msg, false);
        this.clearInputs();
      } catch (err) {
        this.callResponse(err.response.data.message, true);
      }
    },
  },

  mounted() {
    this.getSignupSettings();
    this.getBanner();
    if (this.$route.query.username) {
      this.referral = this.$route.query.username;
    }
  },
  computed: {
    countries() {
      return this.$store.state.registrationDetails.countries;
    },
    FILE_URL() {
      return this.$store.state.fileURL;
    },
  },
  components: { HomeFooter, HomeNavigation },
};
</script>

<style>
.fileInput {
  width: 0.1px;
  height: 0.1px;
  z-index: -1;
  overflow: hidden;
  opacity: 0;
}

.form-input label {
  opacity: 0;
  transition: all 0.4s;
  font-size: 12px;
  font-weight: 200;
}

.form-input label.error {
  color: rgb(254, 50, 50);
  opacity: 1;
}

.div-block-46.active .dot {
  background: #ffb426;
  width: 10px;
  height: 10px;
}

.div-block-46 {
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
}

a.terms {
  font-weight: bold;
  color: #ffb426;
}

.sign-label.response {
  background: transparent;
  width: 100%;
}
.sign-label.bottom {
  width: 100%;
}

.box-line {
  cursor: pointer;
}
</style>
