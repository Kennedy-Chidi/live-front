<template>
  <div id="footer" class="dashboard-footer">
    <div>
      {{ new Date().getFullYear() }} Copyright {{ company.companyName }}, All
      Rights Reserved.
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      company: "",
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
      } catch (err) {
        console.log(err.response.data);
      }
    },
  },
  mounted() {
    this.setFileURL();
    this.loadScript();
    this.getCompany();
  },
};
</script>

<style></style>
