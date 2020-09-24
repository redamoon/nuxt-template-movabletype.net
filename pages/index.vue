<template>
  <div class="list">
    <div v-for="(post, index) in posts" :key="index" class="item">
      <a :href="`/blog/${post.id}`">
        <h2 class="title">{{ post.title }}</h2>
        <p>{{ post.date | formatDate }}</p>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, $config, error }) {
    try {
      const {
        data: { items },
      } = await $axios.get(`${$config.apiUrl}71803/entries`)
      return {
        posts: items,
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
.list {
  width: 600px;
  margin: 20px auto 0;
}
.item {
  border-radius: 5px;
  background: #e5e5e5;
  margin-bottom: 20px;
}
.item > a {
  padding: 10px;
  box-sizing: border-box;
  display: block;
  text-decoration: none;
  color: #000;
}
.title {
  margin: 0;
  padding: 0;
}
</style>
