<template>
    <div>
        <h1> Rock, Paper, Scissors </h1>
        <label for="userSelection"> Choose ROCK, PAPER, or SCISSORS: </label>
        <input v-model="userSelection" @input="validateInput" placeholder="ROCK, PAPER, SCISSORS"/>
        <button @click="playGame">Play</button>
        <p v-if="errorMessage"> {{ errorMessage }} </p>
        <div v-if="result">
            <p> User Selected: {{ userSelection }} </p>
            <p> Computer Selected: {{ computerSelection }} </p>
            <p> {{ result }} </p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'App',
    data() {
        return {
            userSelection: "",
            computerSelection: "",
            result: "",
            errorMessage: "",
        };
    },

    methods: {
        validateChoice(choice) {
            const validChoices = /^(ROCK|PAPER|SCISSORS)$/i;
            if(!validChoices.test(choice)) {
                this.errorMessage = "Please choose ROCK, PAPER, or SCISSORS.";
                return false;
            }
            this.errorMessage = "";
            return true;
        },

        validateInput() {
            this.validateChoice(this.userSelection);
        },

        playGame() {
            if (!this.validateChoice(this.userSelection)) {
                return;
            }

            const randomNumber = Math.random();
            if(randomNumber <= 0.34) {
                this.computerSelection = "ROCK";
            }
            else if(randomNumber <= 0.67) {
                this.computerSelection = "PAPER";
            }
            else {
                this.computerSelection = "SCISSORS";
            }

            const userChoice = this.userSelection.toUpperCase();
            if (userChoice === this.computerSelection) {
                this.result = "It is a tie!";
            }
            else if (
                (userChoice === "ROCK" && this.computerSelection == "SCISSORS") ||
                (userChoice === "PAPER" && this.computerSelection == "ROCK") ||
                (userChoice === "SCISSORS" && this.computerSelection == "PAPER")
            ) {
                this.result = "User Wins!";
            }
            else {
                this.result = "Computer Wins!";
            }
        },
    }
}
</script>