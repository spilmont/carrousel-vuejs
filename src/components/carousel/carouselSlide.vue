<template>
    <transition :name="transition">
<div v-show="visible">
    <slot></slot>

</div>
    </transition>
</template>

<script>
    export default {
        name: "carouselSlide",
        props:{
            index:{type: Number, default:0}
        },
        computed:{

            transition () {
                if(this.$parent.direction){
                return 'slide-'+ this.$parent.direction
                }
            },

            visible(){
                return this.index === this.$parent.index
            }
        }
    }
</script>

<style scoped>

    .slide-right-enter-active{

        animation: slideRightIn 2s;


    }

    .slide-right-leave-active{

        animation: slideRightOut 2s;
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        width: 100%;
    }



    @keyframes slideRightIn {

        from{transform: translateX(100%);}
        to{transform: translateX(0);}


    }

    @keyframes slideRightOut {

        from{transform: translateX(0);}
        to{transform: translateX(-100%);}


    }


    .slide-left-enter-active{

        animation: slideLeftIn .5s;


    }

    .slide-left-leave-active{

        animation: slideLeftOut .5s;
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        width: 100%;
    }



    @keyframes slideLeftIn {

        from{transform: translateX(-100%);}
        to{transform: translateX(0);}


    }

    @keyframes slideLeftOut {

        from{transform: translateX(0);}
        to{transform: translateX(100%);}


    }


</style>
