<template>
  <div>
    <div class="top-header">
      <div class="custom-container">
        <div class="top-header-flex">
          <div class="top-header-right">
            <div class="each-top-right">
              <img
                src="https://uploads-ssl.webflow.com/64584677a42c076b5ad19e3c/645851494312bb2ad82f00e6_envelope.svg"
                loading="lazy"
                alt=""
                class="top-right-img"
              />
              <div>info@tradinglivelimited.com</div>
            </div>
            <div class="each-top-right">
              <img
                src="https://uploads-ssl.webflow.com/64584677a42c076b5ad19e3c/64585500e35d2883c5f0ab09_clock.svg"
                loading="lazy"
                alt=""
                class="top-right-img"
              />
              <div>Mon - Sun : 8:00 - 17:30</div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div
      data-animation="default"
      data-collapse="medium"
      data-duration="400"
      data-easing="ease"
      data-easing2="ease"
      role="banner"
      class="client-navbar w-nav"
    >
      <div class="custom-container">
        <div class="nav-flex">
          <div>
            <nuxt-link
              :to="{
                path: '/',
                query: { username: $route.query.username },
              }"
              class="brand w-nav-brand home-logo"
              ><img src="/Logo.png" loading="lazy" alt="" class="brand-img"
            /></nuxt-link>
            <div id="ytWidget"></div>
          </div>

          <nav role="navigation" class="nav-menu w-nav-menu">
            <nuxt-link
              :to="{
                path: '/',
                query: { username: $route.query.username },
              }"
              class="nav-link w-nav-link"
              >Home</nuxt-link
            ><nuxt-link
              :to="{
                path: '/about',
                query: { username: $route.query.username },
              }"
              class="nav-link w-nav-link"
              >About</nuxt-link
            >
            <nuxt-link
              :to="{
                path: '/plan',
                query: { username: $route.query.username },
              }"
              class="nav-link w-nav-link"
              >Plan</nuxt-link
            ><nuxt-link
              :to="{
                path: '/faq',
                query: { username: $route.query.username },
              }"
              class="nav-link w-nav-link"
              >FAQ</nuxt-link
            ><nuxt-link
              :to="{
                path: '/contact',
                query: { username: $route.query.username },
              }"
              class="nav-link w-nav-link"
              >Contact</nuxt-link
            ><nuxt-link
              :to="{
                path: '/news',
                query: { username: $route.query.username },
              }"
              class="nav-link w-nav-link"
              >Blog</nuxt-link
            >
            <nuxt-link
              v-if="isAuthenticated"
              to="/dashboard"
              class="nav-link w-nav-link"
              >Dashboard</nuxt-link
            >
            <nuxt-link
              v-else
              :to="{
                path: '/signup',
                query: { username: $route.query.username },
              }"
              class="nav-link w-nav-link"
              >Sign up</nuxt-link
            >
            <span
              v-if="isAuthenticated"
              @click="logout"
              class="nav-link btn w-nav-link"
              >Logout</span
            >
            <nuxt-link
              v-else
              :to="{
                path: '/login',
                query: { username: $route.query.username },
              }"
              class="nav-link btn w-nav-link"
              >Login</nuxt-link
            >
          </nav>
          <div class="top-menu w-nav-button">
            <div class="w-icon-nav-menu"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    async logout() {
      await this.$auth.logout();
      this.$router.push("/");
    },
  },
  computed: {
    isAuthenticated() {
      return this.$store.getters.isAuthenticated; // it check if user isAuthenticated
    },
  },
};
</script>

<style>
.nav-link.login {
  color: #00040f;
  background-color: #00f6ff;
  border-radius: 10px;
  padding: 10px 20px;
  font-weight: 600;
}

.top-menu.w-nav-button {
  width: 60px;
}

.home-logo {
  width: 150px;
}
</style>
