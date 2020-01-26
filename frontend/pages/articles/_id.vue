<template>
  <div>

    <div v-if="article.Zdjecie" id="banner"
      class="uk-height-small uk-flex uk-flex-center uk-flex-middle uk-background-cover uk-light uk-padding"
      :data-src="'http://localhost:1337' + article.Zdjecie.url" uk-img>
      <h1>{{ article.title }}</h1>
    </div>

    <div class="uk-section">
      <div class="uk-container uk-container-small">
        <div v-if="article.Tekst" id="editor" v-html="$md.render(article.Tekst)"></div>
        <p v-if="article.Opublikowano">{{ moment(article.Opublikowano).format("MMM Do YY") }}</p>
      </div>
    </div>

  </div>
</template>

<script>
  import articleQuery from '~/apollo/queries/articles/article'
  var moment = require('moment')

  export default {
    data() {
      return {
        article: {},
        moment: moment,
      }
    },
    apollo: {
      article: {
        prefetch: true,
        query: articleQuery,
        variables() {
          return {
            id: parseInt(this.$route.params.id)
          }
        }
      }
    }
  }

</script>
