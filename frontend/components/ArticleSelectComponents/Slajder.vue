<template>
    <div>
        <h4>slajder</h4>
        <div class="slajder" v-for="singleUrl in renderSlider" :key="singleUrl" >
            <img :src="'http://localhost:1337'+singleUrl" alt="" style="width:50px; height:50px">    
        </div> 
       
    </div>
</template>

<script>
export default {
    props:{
        componentData: Object
    },
    computed: {
        renderSlider(){
            const sliderUrls = [];
            this.componentData.SlajderZdjecia.forEach( singleSlide =>{
                sliderUrls.push(singleSlide.url)
            })      
            return sliderUrls
        }
    },

}
</script>