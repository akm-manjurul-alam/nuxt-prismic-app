<template>
  <section class="container">
    <h1>{{ title }}</h1>
    <div>{{ content }}</div>
  </section>
</template>

<script>
import Prismic from 'prismic-javascript'
import { initApi, generatePageData } from '@/prismic.config'

export default {
  asyncData(context) {
    if (context.payload) {
      return generatePageData('homepage', context.payload.data)
    } else {
      return initApi().then(api => {
        return api
          .query(Prismic.Predicates.at('document.type', 'homepage'))
          .then(response => {
            return generatePageData('homepage', response.results[0].data)
          })
      })
    }
  }
}
</script>
