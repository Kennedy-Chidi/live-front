<template>
  <div class="div-block-51">
    <div class="div-block-53">
      <h1 class="heading-38">RECENT POSTS</h1>
      <div class="div-block-52"></div>
      <div v-for="blog in blogs" :key="blog._id">
        <nuxt-link
          :to="`/news-details/${blog._id}`"
          class="link-block-10 w-inline-block"
          ><h1 class="heading-40">{{ blog.title }}</h1></nuxt-link
        >
        <h1 class="heading-41">{{ formatDate(blog.time) }}</h1>
        <div class="div-block-52"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      blogs: [],
    };
  },
  methods: {
    formatDate(data) {
      const date = new Date(data).getTime(); // Note that month is zero-indexed in JavaScript
      const options = {
        year: "numeric",
        month: "long",
        day: "numeric",
        suffix: (day) => {
          if (day === 1 || day === 21 || day === 31) {
            return "st";
          } else if (day === 2 || day === 22) {
            return "nd";
          } else if (day === 3 || day === 23) {
            return "rd";
          } else {
            return "th";
          }
        },
      };

      return new Intl.DateTimeFormat("en-US", options).format(date);
    },

    async getBlogs() {
      try {
        const result = await this.$axios.get("/blog");
        this.blogs = result.data.data;
      } catch (err) {
        console.log(err.response);
      }
    },
  },
  mounted() {
    this.getBlogs();
  },
};
</script>

<style></style>
