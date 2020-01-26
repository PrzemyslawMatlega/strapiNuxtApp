<template>  
  <div>
      <div class="" v-for="(singlePost, index) in renderPosts" :key="index">
              <h2>{{singlePost[0]}}</h2>
              <h4>{{singlePost[1]}}</h4>
              
              <div class="components">
                  <div v-for="(component, index) in singlePost[2]" :key="index" style="padding: 20px; border: 2px solid black; margin: 2rem 0; width: 600px">
                        <component :is="component.componentName" :componentData="component.singleComponent"></component>
                        <!-- {{component.singleComponent}} -->
                  </div>

              </div>


      </div>
      
  </div>
</template>

<script>  
  import Galeria from '~/components/ArticleSelectComponents/Galeria'
  import PoleTekstoweVue from './ArticleSelectComponents/Pole-tekstowe.vue'
  import SlajderVue from './ArticleSelectComponents/Slajder.vue'
  
export default {  
  props: {
    articles: Array
  },
  computed: {
    renderPosts(){
      const allPostsToRender = []
      this.articles.forEach(singlePost =>{
        const singlePostData = [singlePost.Tytul, singlePost.created_at]
        const allComponents = []

        singlePost.KomponentyDynamiczne.forEach( singleComponent => {
            const componentName = singleComponent.__component.split('.')[1]
            allComponents.push({
              componentName,
              singleComponent
            })
        })
        singlePostData.push(allComponents)
        allPostsToRender.push(singlePostData)

      })
      return allPostsToRender
    }
  },
  components:{
    'slajder': SlajderVue,
    'pole-tekstowe': PoleTekstoweVue,
    'galeria': Galeria

  }
}
</script>  