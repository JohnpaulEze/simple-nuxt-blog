<template>
  <div class="max-w-3xl mx-auto min-h-screen my-12">
    <div v-if="post">
      <h1 class="text-2xl font-semibold mb-6">{{ post.title }}</h1>
      <nuxt-content :document="post" />
      <div class="mt-8">
        <nuxt-link
          to="/"
          class="active:bg-green-700 bg-green-500 rounded text-white font-bold py-3 px-5"
          >Back to blog</nuxt-link
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      post: null
    };
  },
  async fetch() {
    this.post = (
      await this.$content()
        .where({ slug: this.$route.params.slug })
        .limit(1)
        .fetch()
    )?.[0];
  }
};
</script>
