<template>
  <div class="wrapper">
    <h2 class="title">{{ post.title }}</h2>
    <p>{{ post.date | formatDate }}</p>
    <!-- eslint-disable-next-line vue/no-v-html-->
    <div class="body" v-html="post.body"></div>
    <a href="/">トップ</a>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, $config, params, error }) {
    try {
      const { data } = await $axios.get(
        `${$config.apiUrl}${$config.blogId}/entries/${params.id}`
      )
      return {
        post: data,
      }
    } catch (err) {
      error({
        errorCode: 404,
      })
    }
  },
}
</script>

<style>
.wrapper {
  width: 600px;
  margin: auto;
}
.title {
  font-size: 30px;
}
.body {
  font-size: 20px;
}
</style>
