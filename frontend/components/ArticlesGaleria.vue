<template>
    <div>
        <div class="" v-for="article in articles" :key="article.id">
               <span>{{article.id}}</span>
               <div>{{article.Tytul}}</div>
                <div class="">Galeria</div>
                <div class="" v-for="galeria in article.GaleriaKomponent" :key="galeria[0]">
                        
                     {{galeria}}
                
                </div>

        </div>
    </div>
</template>

<script>
export default {
    props:{
        articles: Array
    },
    computed: {
        renderArticles(){
            console.log('hello')
            console.log(this.articles)
        }
    },
}
</script>