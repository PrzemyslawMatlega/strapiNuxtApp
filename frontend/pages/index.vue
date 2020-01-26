<template>
  <div>

    <div class="uk-section">
      <div class="uk-container uk-container-large">
        <h2>Strapi blog</h2>
        <br>

        <h3>Base Articles</h3>
        <Articles :articles="articles"></Articles>
        <br>
        <br>
        <hr>
        <h3>Articles Galeria</h3>
        <ArticlesGalery :articles="artykulGalerias"></ArticlesGalery>
        <br>
        <br>
        <hr>
        <h3>Articles Select</h3>
        <hr>
        <ArticlesSelect :articles="artykulSelects"/>
      </div>
    </div>

  </div>
</template>

<script>
  import articlesQuery from '~/apollo/queries/articles/articles'
  import ArticlesSelectQuery from '~/apollo/queries/articlesSelect/articlesSelect'
  import ArticlesGaleriaQuery from '~/apollo/queries/articlesGalery/articlesGalery'
  import ArticlesGalery from '~/components/ArticlesGaleria'
  import ArticlesSelect from '~/components/ArticlesSelect'
  import Articles from '~/components/Articles'

  export default {
    data() {
      return {
        articles: [],
        artykulGalerias: [],
        artykulSelects: [],
       
      }
    },
    mounted() {
      fetch('http://localhost:1337/artykul-selects')
        .then(response => response.json())
        .then(myResponse => {
          const responseArr =[]
          myResponse.forEach( singlePost => {
            responseArr.push(singlePost)
          })
          this.artykulSelects = responseArr
          
        })
    },
    components: {
      Articles,
      ArticlesSelect,
      ArticlesGalery
    },
    apollo: {
      articles: {
        prefetch: true,
        query: articlesQuery,
        variables() {
          return {
            id: parseInt(this.$route.params.id)
          }
        }
      },
      artykulGalerias: {
        prefetch: true,
        query: ArticlesGaleriaQuery,
      },
      //  artykulSelects :{
      //   prefetch:true,
      //   query: ArticlesSelectQuery,
      //   variables () {
      //     return { id: parseInt(this.$route.params.id) }
      //   }
      // }
    }
  }

</script>
