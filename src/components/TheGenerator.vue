<template>
  <div class="hello">
      <h1>{{ msg }}</h1>

      <h2>Options:</h2>
      <div class="options-container">
        <div class="options">
          <span class="option-label">
            <label class="block" for="genres">Genres</label>
            <input v-model="options.genres" type="number" id="genres">
          </span>

          <span class="option-label">
            <label class="block" for="nouns">Stuffs</label>
            <input v-model="options.nouns" type="number" id="nouns">
          </span>

          <span class="option-label">
            <label class="block" for="adjectives">Fanciness</label>
            <input v-model="options.adjectives" type="number" id="adjectives">
          </span>

          <span class="option-label">
            <label class="block" for="verbs">Actions</label>
            <input v-model="options.verbs" type="number" id="verbs">
          </span>
        </div>
      </div>

      <h2>Game idea:</h2>
      <p>{{ idea }}</p>
      <button @click="makeSentence">Generate!</button>
  </div>
</template>

<script>
import Sentencer from 'sentencer'

export default {
  name: 'TheGenerator',
  props: {
    msg: String
  },
  data () {
    return {
      options: {
        genres: 1,
        nouns: 1,
        adjectives: 1,
        verbs: 1
      },
      idea: '',
      gameGenres: [
        'A Platformer',
        'A Shooter',
        'A Fighting',
        "A Beat 'em up",
        'A Stealth',
        'A Survival',
        'A Rhythm',
        'A Survival horror',
        'A Metroidvania',
        'A Text adventure',
        'A Graphic adventure',
        'A Visual novel',
        'An Interactive movie',
        'A Real-time 3D adventure',
        'An Action RPG',
        'An MMORPG',
        'A Roguelike',
        'A Tactical RPG',
        'A Sandbox RPG',
        'A First-person party-based RPG',
        'A Choices',
        'A Fantasy',
        'A Construction and management simulation',
        'A Life simulation',
        'A Vehicle simulation',
        'A 4X',
        'An Artillery',
        'A Real-time strategy (RTS)',
        'A Real-time tactics (RTT)',
        'A Multiplayer online battle arena (MOBA)',
        'A Tower defense',
        'A Turn-based strategy (TBS)',
        'A Turn-based tactics (TBT)',
        'A Wargame',
        'A Racing',
        'A Sports',
        'A Sports-based fighting',
        'An MMO',
        'A Casual',
        'A Party',
        'A Programming',
        'A Logic',
        'A Trivia',
        'A Board',
        'A Card',
        'An Idle game'
      ]
    }
  },
  methods: {
    makeSentence () {
      this.idea = Sentencer.make('{{ a_genre }}/{{ genre }} game where you collect {{ adjective }} {{ nouns }}.')
    }
  },
  created () {
    let getGenre = () => {
      return this.gameGenres[Math.floor(Math.random() * this.gameGenres.length)]
    }

    Sentencer.configure({
      actions: {
        a_genre: getGenre,
        genre () {
          return getGenre().split(' ').splice(1, 2).join(' ')
        }
      }
    })
  }
}
</script>

<style scoped>
.options {
  display: flex;
}

.option-label {
  margin: 0 8px;
}

.block {
  display: block
}
</style>
