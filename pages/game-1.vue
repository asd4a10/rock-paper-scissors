<template>
  <v-row>
    <v-col class="text-center">
      <blockquote class="blockquote">
        &#8220;Life is not a game of luck. If you wanna win, work hard.&#8221;
        <div>
          <small>
            <em>&mdash;Sora</em>
          </small>
        </div>
      </blockquote>
      <br />
      <div>Score: {{ human }} - {{ computer }}</div>
      <v-btn v-if="!game_active" class="mb-5" elevation="2" @click="startGame"
        >Play round</v-btn
      >
      <br />
      <div v-if="game_active">
        <div>
          <div class="d-flex justify-space-around">
            <v-hover
              v-if="human_choice === ''"
              value="true"
              v-for="choice in choices"
            >
              <v-card @click="humanTurn(choice)" :class="{ 'on-hover': hover }">
                <v-card-title>{{ choice }}</v-card-title>
                <v-icon large>{{ icons[choice] }}</v-icon>
              </v-card>
            </v-hover>
            <v-card v-if="human_choice !== ''">
              <v-card-title>{{ human_choice }}</v-card-title>
              <v-icon large>{{ icons[human_choice] }}</v-icon>
            </v-card>
            <v-card v-if="computer_choice !== ''">
              <v-card-title>{{ computer_choice }}</v-card-title>
              <v-icon large>{{ icons[computer_choice] }}</v-icon>
            </v-card>
          </div>
        </div>
        <div class="my-5" v-if="result !== ''">{{ result }}</div>
        <br />
        <v-btn elevation="2" @click="endGame">End round</v-btn>
      </div>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'InspirePage',
  data() {
    return {
      human: 0,
      computer: 0,
      game_active: false,
      human_choice: '',
      computer_choice: '',
      choices: ['paper', 'scissors', 'rock'],
      icons: {
        paper: 'mdi-note',
        scissors: 'mdi-content-cut',
        rock: 'mdi-google-cloud',
      },
      result: '',
    }
  },
  methods: {
    startGame() {
      this.game_active = true
    },
    humanTurn(choice) {
      this.human_choice = choice
      this.computerTurn()
      this.calculateResult()
    },
    computerTurn() {
      const index = Math.floor(Math.random() * 3)
      this.computer_choice = this.choices[index]
    },
    calculateResult() {
      switch (this.human_choice + this.computer_choice) {
        case 'paperscissors':
          this.result = 'computer wins'
          break
        case 'scissorspaper':
          this.result = 'human wins'
          break
        case 'rockscissors':
          this.result = 'human wins'
          break
        case 'scissorsrock':
          this.result = 'computer wins'
          break
        case 'paperrock':
          this.result = 'human wins'
          break
        case 'rockpaper':
          this.result = 'computer wins'
          break
        default:
          this.result = 'draw'
      }
      if (this.result === 'computer wins') {
        this.computer += 1
      } else if (this.result === 'human wins') {
        this.human += 1
      }
    },
    endGame() {
      this.human_choice = ''
      this.computer_choice = ''
      this.result = ''
      this.game_active = false
    },
  },
}
</script>
