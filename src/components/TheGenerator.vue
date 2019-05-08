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
import sentencer from 'sentencer'

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
        'Platformer',
        'Shooter',
        'Fighting',
        "Beat 'em up",
        'Stealth',
        'Survival',
        'Rhythm',
        'Survival horror',
        'Metroidvania',
        'Text adventure',
        'Graphic adventure',
        'Visual novel',
        'Interactive movie',
        'Real-time 3D adventures',
        'Action RPG',
        'MMORPG',
        'Roguelike',
        'Tactical RPG',
        'Sandbox RPG',
        'First-person party-based RPG',
        'Choices',
        'Fantasy',
        'Construction and management simulation',
        'Life simulation',
        'Vehicle simulation',
        '4X',
        'Artillery',
        'Real-time strategy (RTS)',
        'Real-time tactics (RTT)',
        'Multiplayer online battle arena (MOBA)',
        'Tower defense',
        'Turn-based strategy (TBS)',
        'Turn-based tactics (TBT)',
        'Wargame',
        'Racing',
        'Sports',
        'Sports-based fighting',
        'MMO',
        'Casual',
        'Party',
        'Programming',
        'Logic',
        'Trivia',
        'Board',
        'Card',
        'Idle game'
      ]
    }
  },
  methods: {
    makeSentence () {
      this.idea = sentencer.make('An FPS/RPG game where you collect {{ adjective }} {{ nouns }}.')
    }
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
