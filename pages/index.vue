<template>
  <div>
    <div v-for="(entry, index) in entries" :key="index">
      <h2>{{ entry.title }}</h2>
      <p>{{ entry.date }}</p>
      <p>{{ entry.id }}</p>
      <a :href="`/blog/${entry.id}`">記事詳細</a>
      <div v-html="entry.body"></div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  async asyncData({ $config, error }) {
    try {
      const { data } = await axios.get(`${$config.apiUrl}71803/entries`)
      // const { items } = data
      return {
        entries: data.items,
      }
    } catch (err) {
      error({
        errorCode: 404,
      })
    }
  },
}
</script>
