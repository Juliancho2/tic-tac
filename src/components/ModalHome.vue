<template>
    <div class="modal_home" v-show="actionGame">
        <div class="option_figure">
            
            <h2>Escoge una figura</h2>
            <h4>{{gameOver}}.</h4>
            <div class="item_figure">
                <div class="circle figure " @click="actionSelectedFigure('circle')">
                    <img src="../assets/circle.png" alt="">
                </div>
                <div class="equis figure" @click="actionSelectedFigure('cicle')">
                    <img src="../assets/equis.png" alt="">
                </div>
            </div>
        </div>
    </div>
</template>
<style scoped>
* {
    font-family: sans-serif;
    color: rgb(41, 38, 38);
}
.modal_home {
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    background: rgba(59, 54, 64, 0.693);
    z-index: 20;
    width: 100%;
    height: 100%;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
}

.option_figure {
    background: rgb(222, 219, 219);
    padding: 20px 10px;
    border-radius: 5px;
    width: 250px;
}

.option_figure h4,.option_figure h2{
    font-weight: 500;
    text-align: center;
}
.item_figure {
    display: grid;
    grid-template-columns: 80px 80px;
    justify-content: center;
    gap: 10px;

}

.circle,
.equis {
    text-align: center;
    padding: 5px;
    box-shadow: 1px -1px 5px -3px rgba(186, 174, 174, 0.75);
    -webkit-box-shadow: 1px -1px 5px -3px rgba(186, 174, 174, 0.75);
    -moz-box-shadow: 1px -1px 5px -3px rgba(186, 174, 174, 0.75);
    background: rgba(184, 184, 183, 0.632);
    border-radius: 3px;
}

.circle img,
.equis img {
    width: 50px;
}
.figure:hover{
    opacity: 0.5;
    transition: all 0.5s;
    cursor: pointer;
}
</style>
<script setup>
import { ref, toRefs, watch } from 'vue';

const props=defineProps({
    gameOver:{
        type:String,
        default:""
    },
    closeModalToGrid:{
        default:false,
    }
   
});
const {closeModalToGrid} = toRefs(props);


//variables reactivas 
const actionGame=ref(true);//cerrar el modal.
const emit =defineEmits(['selectedFigure','changeCloseModalGrid']);

watch(closeModalToGrid,(value)=>{
    actionGame.value=value;
    
    emit('changeCloseModalGrid',"false");
});
//funcion cierre modal y seleccion de figurea
const actionSelectedFigure=function(figure){
    actionGame.value=false;
    figure == 'circle'?emit("selectedFigure","circle")
                    :emit("selectedFigure","equis");
                    
}



</script>
