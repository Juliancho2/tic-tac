<script setup>
import { toRefs, ref, watch } from 'vue';

//Prop traida de Index.
const props = defineProps({
    figureFirstGrid: String,

});
const { figureFirstGrid } = toRefs(props);

//array jugador ganador.
const movementsPlayers = ref([
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]);
//conteo de movimientos de juego.
const countMovements=ref(0);

 
const emit = defineEmits(['emitCloseModal']);


//funcion finalizacion del juego.
const endGame = function () {
    const items = document.querySelectorAll(".item");
    items.forEach(element => {
        if (element.firstChild) {
            element.innerHTML = "";
        }
    });
    movementsPlayers.value = [
        [1, 2, 3],
        [4, 5, 6],
        [7, 8, 9]
    ];
    countMovements.value=0;
    emit('emitCloseModal', true);
}

//declaracion y cambio de variable.
let figureChange;
watch(figureFirstGrid, (value) => figureChange = value);

//funcion validacion de juego
const winnerValidation = function (list) {
    
    //Horizontal.

    if (list[0][0] == list[0][1] && list[0][0] == list[0][2]) {
        setTimeout(() => {
            endGame()
        }, 800)
    }
    if (list[1][0] === list[1][1] && list[1][0] === list[1][2]) {
        setTimeout(() => {
            endGame()
        }, 800)
    }
    if (list[2][0] == list[2][1] && list[2][0] == list[2][2]) {
        setTimeout(() => {
            endGame()
        }, 800)
    }
    //vertical.
    if (list[0][0] == list[1][0] && list[0][0] == list[2][0]) {
        setTimeout(() => {
            endGame()
        }, 800)
    }
    if (list[0][1] == list[1][1] && list[0][1] == list[2][1]) {
        setTimeout(() => {
            endGame()
        }, 800)
    }
    if (list[0][2] == list[1][2] && list[0][2] == list[2][2]) {
        setTimeout(() => {
            endGame()
        }, 800)
    }
    //Diagonal
    if (list[0][0] == list[1][1] && list[0][0] == list[2][2]) {
        setTimeout(() => {
            endGame()
        }, 800)
    }
    if (list[0][2] == list[1][1] && list[0][2] == list[2][0]) {
        setTimeout(() => {
            endGame()
        }, 800)
    }

}
//funcion movimientos del ganador.
const playerWin = function (id, figure) {
    switch (id) {
        case "0": movementsPlayers.value[0][0] = figure;
            break;
        case "1": movementsPlayers.value[0][1] = figure;
            break;
        case "2": movementsPlayers.value[0][2] = figure;
            break;
        case "3": movementsPlayers.value[1][0] = figure;
            break;
        case "4": movementsPlayers.value[1][1] = figure;
            break;
        case "5": movementsPlayers.value[1][2] = figure;
            break;
        case "6": movementsPlayers.value[2][0] = figure;
            break;
        case "7": movementsPlayers.value[2][1] = figure;
            break;
        case "8": movementsPlayers.value[2][2] = figure;
            break;

    };

    winnerValidation(movementsPlayers.value);


}
//funcion agregar figura.
const addFigure = function (e) {
    let itemId = e.target.id;
    if (e.target.matches(".item")) {
        let item = e.target;

        if(countMovements.value == 9){
            endGame();
        }
        
        if (figureChange == 'circle') {
            if (!item.firstChild) {
                item.innerHTML = `<img style="width:60px" class="circle" src="./assets/circle.a1c65350.png" alt=""/>`;
                figureChange = 'equis';
                countMovements.value= countMovements.value + 1;
                console.log(countMovements.value, "haz hecho un movimiento");
            }
        }
        else {
            if (!item.firstChild) {
                item.innerHTML = `<img style="width:60px"src="./assets/equis.1cd86a05.png" alt="">`;
                figureChange = 'circle';
                countMovements.value= countMovements.value + 1;
                console.log(countMovements.value, "haz hecho un movimiento");
            }
        }
    }
    playerWin(itemId, figureChange);
}
</script>

<template>

    <div class="full_container">

        <div class="container_grid">
            <div class="item" id="0" @click="addFigure">

            </div>
            <div class="item" id="1" @click="addFigure">

            </div>
            <div class="item" id="2" @click="addFigure">

            </div>
            <div class="item" id="3" @click="addFigure">

            </div>
            <div class="item" id="4" @click="addFigure">

            </div>
            <div class="item" id="5" @click="addFigure">

            </div>
            <div class="item" id="6" @click="addFigure">

            </div>
            <div class="item" id="7" @click="addFigure">

            </div>
            <div class="item" id="8" @click="addFigure">

            </div>
        </div>
    </div>
</template>

<style scoped>
.full_container {
    display: flex;
    justify-content: center;
    background: #966641;
    min-width: 300px;
    max-width: 500px;
    height: 50vh;
    margin: 30px auto;
    box-shadow: 0px 0px 7px 0px rgba(0,0,0,0.54);
    
}

.container_grid {
    display: grid;
    grid-template-rows: repeat(3, 1fr);
    grid-template-columns: repeat(3, 1fr);
    gap: 5px;
    width: 100%;
    height: 100%;
   
}

.item {
    background: url('../assets/pexels-pixabay-235985.jpg') center/cover no-repeat;
   
    display: flex;
    justify-content: center;
    align-items: center;
 
}
</style>