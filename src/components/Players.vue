<template>
    <div class="container_players">
        <div class="container_players_figure">
            <div class="circle">
                <p>Player one:</p> <img :src="figureRender()" alt=""/>
            </div>
            <div class="equis">
                <p>Player two:</p> <img :src="figureRender() == './assets/circle.a1c65350.png'? 
                './assets/equis.1cd86a05.png':
                './assets/circle.a1c65350.png'"  />
            </div>
        </div>

    </div>
    
</template>
<script setup>
import { toRefs, watch } from 'vue';

    const props= defineProps({
        figurePlayers:String,
    })
    const {figurePlayers}= toRefs(props);

   const wathFigure=watch(figurePlayers,(value)=>{
        figureRender();
    });

   const figureRender=function(){
    return figurePlayers.value == 'circle'? './assets/circle.a1c65350.png': './assets/equis.1cd86a05.png';
   }

   
    
</script>
<style scoped>
html{
    font-size: 10px;
    
}
*{
    font-family: sans-serif;
    color: rgb(0, 0, 0);
    
}
.container_players{
    padding: 20px 0;
    margin: 0 auto;
}
.container_players img{
    width: 40px;
}
.container_players_figure{
    display: grid;
    grid-template-columns: 1fr 1fr;
    justify-content: center;
    min-width: 10rem;
    max-width: 20rem;
    margin: 0 auto;
    background: url('../assets/pexels-pixabay-235985.jpg') center/cover ;
    box-shadow: 0px 0px 7px 0px rgba(0, 0, 0, 0.229);
    padding: 3px 0;
    font-size: 1.1rem;
    font-weight: 500;
}
.circle, .equis{
    text-align: center;
}
</style>