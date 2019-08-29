<template>
    <div class="carousel">
        <slot></slot>
        <span class="carousel__nav carousel__preview" @click.prevent="preview"><</span>
        <span class="carousel__nav carousel__next" @click.prevent="next" @set-time="slideTime">></span>

        <div class="carousel__pagination">
            <button v-for="n in this.slidecount" @click="goto(n-1)" :class="{active: n-1 == index}"></button>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Carousel",

        data (){
            console.log(this.$children);
            return{
                index: 0,
                slides: [],
                direction: 'right',
                timer:''
            }
        },

        mounted() {
            this.slides = this.$children // "this.$children" propritée de vue.js permetant de recuperer les enfant direct du composant
            this.timer = setInterval(this.next,5000)

        },
        watch:{
            slides (slides){
                if (this.index >= this.slidecount){
                    this.index =  this.slidecount - 1;
                }

            }
        },

        methods:{
            next(){
                this.index++;
                this.direction = 'right';
                if (this.index >= this.slidecount){
                    this.index = 0;
                }

            },
            preview(){
                this.index--;
                this.direction = 'left';
                if (this.index < 0){
                    this.index =  this.slidecount - 1;
                }

            },
            slideTime(){

                setTimeout(next,2000)

            },

            goto(index){

                this.direction = index > this.index ? 'right' : 'left';

                this.index = index
            }
        },

        computed:{

            slidecount(){
                return this.slides.length
            },


        },

    }
</script>

<style scoped>
    .carousel{
        position: relative;
        overflow: hidden;
    }
    .carousel__nav{
          position: absolute;
          top: 50%;
          left: 10px;
          font-size: 2em;
          font-weight: bold  ;
            color: white;

      }
    .carousel__nav.carousel__next{

        right: 10px;
        left: auto;

    }

    .carousel__nav.carousel__next:hover{

        font-size: 4em;
        color: red;

    }
    .carousel__nav.carousel__preview:hover{

        font-size: 4em;
        color: red;

    }

    .carousel__pagination{
        position: absolute;
        bottom: 10px;
        left: 0;
        right: 0;
        text-align: center;
    }

    .carousel__pagination button{
        display: inline-block;
        width: 20px;
        height: 20px;
        background-color: black;
        opacity: .7;
        border-radius: 10px;
        margin: 0 2px;

    }

    .carousel__pagination button.active{
        background-color: white;
    }


</style>
