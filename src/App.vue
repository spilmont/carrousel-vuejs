<template>
    <div id="app">
        <carousel>
            <carousel-slide v-for="n in slides" :index="n -1 "  >
                <div style="position:absolute; left: 0; right: 0; text-align: center; top: 50%; color: white; font-size: 32px; font-weight: bold">slide {{n}}</div>
                <img :src="'https://placeimg.com/640/300/tech/'+n" width="100%" height="600px">
            </carousel-slide>
        </carousel>
        <button @click="delSlide" title="supprimer un slide">-</button>
        <button @click="addSlide" title="ajouter un slide">+</button>
    </div>
</template>

<script>


    import Carousel from "./components/carousel/Carousel"
    import CarouselSlide from "./components/carousel/carouselSlide"

    export default {
        name: 'App',
        components: {
            Carousel, CarouselSlide
        },
        data(){
            return{
                slides:5
            }
        },
        methods:{
            addSlide(){
                this.slides++;
            },
            delSlide(){
                this.slides--;
            }
        }
    }
</script>

<style>



    #app {

    }
</style>
