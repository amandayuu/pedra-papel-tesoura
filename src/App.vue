<template>
    <div id="app">
        <div class="container">
            <div class="card-container"
                :class="{ 'draw' : draw, 'win' : win, 'lose' : lose}">
                <div class="header"
                    :class="{ 'draw' : draw, 'win' : win, 'lose' : lose}">
                    <h1>{{ title }} 
                        <img v-show="draw" src="./assets/images/empate.png">
                        <img v-show="win" src="./assets/images/ganhou.png">
                        <img v-show="lose" src="./assets/images/perdeu.png">
                    </h1>
                    
                </div>

                <!-- BODY -->
                <div class="body">   
                    <i  v-show="!started" 
                        class="fas icon fa-gamepad icon-gradient"></i>
                    
                    <div class="in-game" v-show="started">
                        <div class="in-game-content player">

                            <p class="playerText">Jogador</p>

                            <i  class="fas result icon" 
                                :class="actionPlayer"></i> 
                        </div>                   

                        <img src="./assets/images/vs.png">

                        <div class="in-game-content cpu">
                            <p class="cpuText"> CPU</p>
                            <i  class="fas result icon" 
                                :class="actionCPU"></i>
                        </div>
                    </div>

                    <button 
                        class="btn" 
                        v-show="started"
                        @click="restartGame"> 
                        RECOMEÇAR 
                    </button>                

                    <p  class="info-text" 
                        v-show="!started">
                        Faça sua jogada!
                    </p>

                    <div class="footer" v-show="!started">
                        <i  class="fas fa-solid fa-hand-back-fist _rotate icon-footer" 
                            :class="rock" 
                            @click="selected(rock)"></i>

                        <div class="line"></div>

                        <i  class="fas fa-hand _rotate icon-footer" 
                            :class="paper" 
                            @click="selected(paper)"></i>

                        <div class="line"></div>

                        <i  class="fas fa-hand-scissors icon-footer _rotate-180" 
                            :class="scissor" 
                            @click="selected(scissor)"></i>
                    </div>                
                </div>
                <!-- Fim BODY -->

            </div>
        </div>
        
    </div>
</template>

<script>

    export default {
        data(){
            return {
                title: 'Pedra, Papel, Tesoura',
                actionPlayer: '',
                actionCPU: '',
                started: false,
                rock: 'rock',
                scissor: 'scissor',
                paper: 'paper',
                numberCPU: Number,
                draw: false,
                win: false,
                lose: false,
            }
        },

        methods: {
            restartGame() {
                this.started = false   

                this.draw = false
                this.win = false
                this.lose = false

                this.title = 'Pedra, Papel, Tesoura'
                this.numberCPU = Math.floor(Math.random() * 3)
            },

            selected(option) {
                this.started = true
                this.selectedCPU()
                
                if(option == 'rock'){
                    this.actionPlayer = 'fa-hand-back-fist player _rotate'

                    if(this.numberCPU == 0) {
                        this.title = 'Empate!'
                        this.draw = true
                        return
                    }

                    if(this.numberCPU == 1) {
                        this.title = 'Você perdeu!'
                        this.lose = true
                        return
                    }

                    this.title = 'Você venceu!'
                    this.win = true
                    return

                }

                if(option == 'paper'){
                    this.actionPlayer = 'fa-hand player _rotate'

                    if(this.numberCPU == 0) {
                        this.title = 'Você venceu!'
                        this.win = true
                        return
                    }

                    if(this.numberCPU == 1) {
                        this.title = 'Empate!'
                        this.draw = true
                        return
                    }

                    this.title = 'Você perdeu!'
                    this.lose = true
                    return
                }

                if(option == 'scissor'){
                    this.actionPlayer = 'fa-hand-scissors player _rotate-180'

                    if(this.numberCPU == 0) {
                        this.title = 'Você perdeu!'
                        this.lose = true
                        return
                    }

                    if(this.numberCPU == 1) {
                        this.title = 'Você ganhou!'
                        this.win = true
                        return
                    }

                    this.title = 'Empate!'
                    this.draw = true
                    return
                }
            },

            selectedCPU(){
                // Pedra
                if(this.numberCPU == 0){
                    this.actionCPU = 'fa-hand-back-fist cpu _rotate-inverse'
                }

                // Papel
                if(this.numberCPU == 1){
                    this.actionCPU = 'fa-hand cpu _rotate-inverse'
                }

                // Tesoura
                if(this.numberCPU == 2){
                    this.actionCPU = 'fa-hand-scissors cpu'
                }
            }
        },

        mounted() {            
            this.numberCPU = Math.floor(Math.random() * 3)
        }
    }
</script>

<style lang="scss">
    @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600&family=Montserrat:wght@400;600&display=swap');
    @import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.2.0/css/all.min.css');

    #app {
        display: grid;
        justify-items: center;
    }

    .container {
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
    }

    .card-container {
        font-family: Inter, Helvetica, Arial, sans-serif;
        position: relative;
        width: 500px;
        height: 467px;
        border-radius: 8px;
        background: #fff;

        &.draw {
            &:before {
                background: #3A2A45;
            }
        }

        &.win {
            &:before {
                background: #00A78E;
            }
        }

        &.lose {
            &:before {
                background: #E35858;
            }
        }

        &:before {
            content: '';
            position: absolute;
            top: 0;
            right: 0;
            left: 0;
            bottom: 0;
            z-index: -1;
            border-radius: 10px;
            margin: -2px;
            background: linear-gradient(84.45deg, #961EF4 0%, #E35858 100%);
        }
        
        .header {
            position: absolute;
            top: 0;
            left: -5px;
            right: -5px;
            z-index: 1;
            border-radius: 10px;
            height: 100px;
            background: linear-gradient(84.45deg, #961EF4 0%, #E35858 100%);


            &.draw {
                background: #3A2A45;
            }

            &.win {
                background: #00A78E;
            }

            &.lose {
                background: #E35858;
            }
        
            h1 {
                padding: 0;
                display: flex;
                margin: 0;
                justify-content: center;
                padding-top: 30px;
                color: #fff;
                font-weight: 900;
            }
        }        

        .body {
            padding-top: 100px;
            box-sizing: border-box;
            height: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;

            .in-game {
                display: flex;
                align-items: center;
                margin-bottom: 20px;

                .in-game-content {
                    display: flex;
                    flex-direction: column;
                    &.player {
                        padding-right: 64px;
                    }

                    &.cpu {
                        padding-left: 64px;
                    }

                    .playerText {
                        font-size: 15px;
                        color: #961EF4;
                        font-weight: 700;
                    }

                    .cpuText {
                        font-size: 15px;
                        color: #E35858;
                        font-weight: 700;
                    }

                    .cpu {
                        color: #E35858;
                    }

                    .player {
                        background: #961EF4;
                        -webkit-background-clip: text;
                        -webkit-text-fill-color: transparent;
                    }
                }
            }

            .icon {
                font-size: 60px;
            }

            .result {
                font-size: 60px;
            }

            .icon-gradient {
                background: linear-gradient(84.45deg, #961EF4 0%, #E35858 100%);
                -webkit-background-clip: text;
                -webkit-text-fill-color: transparent;
            }

            .btn {
                background: #00A78E;
                border: 2px solid #00A78E;
                border-radius: 100px;
                cursor: pointer;
                color: #fff;
                width: 150px;
                height: 38px;
                font-weight: 700;
            }

            .info-text {
                font-weight: 700;
                font-size: 20px;
                background: linear-gradient(84.45deg, #961EF4 0%, #E35858 100%);
                -webkit-background-clip: text;
                -webkit-text-fill-color: transparent;
            }

            .footer {
                background: #3A2A45;
                height: 92px;
                width: 380px;
                border-radius: 10px;
                margin-top: 30px;
                display: flex;
                flex-direction: row;
                align-items: center;
                justify-content: space-evenly;
                cursor: pointer;

                .icon-footer {
                    font-size: 60px;
                    background: #fff;
                    -webkit-background-clip: text;
                    -webkit-text-fill-color: transparent;

                    &:hover {
                        background-color: #961EF4;
                    }
                }

                .line {
                    border-left: 2px solid #fff;
                    height: 40px;
                }
            }
        }
    }

    ._mirrored {
        transform: scaleX(-1);
    }

    ._rotate {
        transform: rotate(90deg);
    }

    ._rotate-inverse {
        transform: rotate(-90deg);
    }

    ._rotate-180 {
        transform: rotate(180deg);
    }

</style>