<template>
  <div>
    <h2>{{ entry.title }}</h2>
    <div v-html="entry.body"></div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  async asyncData({ $config, params, error }) {
    try {
      const { data } = await axios.get(
        `${$config.apiUrl}71803/entries/${params.id}`
      )
      return {
        entry: data,
      }
    } catch (err) {
      error({
        errorCode: 404,
      })
    }
  },
}
</script>
