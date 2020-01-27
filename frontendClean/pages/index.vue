<template>
  <div>
        <br>
        <hr>
        <h3>Articles Select</h3>
        <hr>
        <ArticlesSelect :articles="artykulSelects"/>
 
  </div>
</template>

<script>
  import ArticlesSelect from '~/components/ArticlesSelect'

  export default {
    data() {
      return {
  
      }
    },
    asyncData(context){
          return fetch('http://localhost:1337/artykul-selects')
        .then(response => response.json())
        .then(myResponse => {
          const responseArr =[]
          myResponse.forEach( singlePost => {
            responseArr.push(singlePost)
          })
          console.log(responseArr)

          return{
            artykulSelects:responseArr
          }
        })
    },
    components: {
      ArticlesSelect,
    },
  
  }

</script>
