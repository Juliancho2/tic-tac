<script setup>
import { ref } from 'vue';
import ModalHome from './ModalHome.vue';
import Players from './Players.vue';
import GridContainer from './GridContainer.vue';
//variable reactiva que enviara el player
const figureSelectedPlayer = ref("");
const closeModalToGrid = ref(false);
const messageEndgame = ref("")
//emit del componente ModalHome
const selectedFigure = function (value) {
    figureSelectedPlayer.value = value;
}
const emitCloseModal = (value) => {
    closeModalToGrid.value = value;
    messageEndgame.value = "Juego terminado"

}
const changeCloseModalGrid = (value) => {
    closeModalToGrid.value = value;
}


</script>
<template>
    <div class="index_home">

        <h2>Tic tac</h2>

        <div class="modal_option">
            <ModalHome @selectedFigure="selectedFigure" :closeModalToGrid="closeModalToGrid" :game-over="messageEndgame"
                @changeCloseModalGrid="changeCloseModalGrid" />
        </div>
        <div class="players_containers">
            <Players :figurePlayers="figureSelectedPlayer"></Players>
        </div>
        <div class="grid_container">
            <GridContainer :figureFirstGrid="figureSelectedPlayer" @emitCloseModal="emitCloseModal" />


        </div>

    </div>
</template>
<style scoped>
* {
    box-sizing: border-box;
}

.index_home {
    position: relative;
    background:#ebf0f2;
    height: 100%;
    width: 100%;
    font-family: sans-serif;
    padding-left: 10px;
    padding-right: 10px;

}

h2 {
    font-size: 3rem;
    margin: 0;
    text-align: center;
    padding-top: 50px;
    color: rgb(22, 19, 19);
}
</style>