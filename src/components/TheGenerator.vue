<template>
  <div class="hello">
      <h1>{{ msg }}</h1>

      <h2>Options:</h2>
      <div class="options-container">
        <div class="options">
          <span class="option-label">
            <label class="block" for="genres">Genres</label>
            <input v-model="genres" type="number" id="genres" min="1" :max="gameGenres.length">
          </span>

          <span class="option-label">
            <label class="block" for="fancyTopics">Fancy?</label>
            <input v-model="fancyTopics" type="checkbox" id="fancyTopics">
          </span>

          <span class="option-label">
            <label class="block" for="topics">Topics</label>
            <input v-model="topics" type="number" id="topics">
          </span>

          <span class="option-label">
            <label class="block" for="fancyActions">Fancy?</label>
            <input v-model="fancyActions" type="checkbox" id="fancyActions">
          </span>

          <span class="option-label">
            <label class="block" for="actions">Actions</label>
            <input v-model="actions" type="number" id="actions">
          </span>
        </div>
      </div>

      <h2>Game idea:</h2>
      <p>{{ idea }}</p>
      <p>
        <idea-fragment :fragment="genGenre()" />
        game about
        <idea-fragment>topics</idea-fragment>
        where you must
        <idea-fragment>actions</idea-fragment>.
      </p>
      <button @click="makeSentence">Generate!</button>
  </div>
</template>

<script>
import Verbs from '@/assets/verbs.js'
import Sentencer from 'sentencer'

import IdeaFragment from '@/components/IdeaFragment'

export default {
  name: 'TheGenerator',
  props: {
    msg: String
  },
  components: {
    IdeaFragment
  },
  data () {
    return {
      genres: 1,
      fancyTopics: true,
      topics: 1,
      MAX_TOPICS: 10,
      fancyActions: true,
      actions: 1,
      MAX_ACTIONS: 10,
      idea: {
        genres: {
          join: (words) => words.join(' / '),
          words: []
        },
        topics: {
          join: (words) => words.length === 1 ? words[0] : words.splice(0, words.length - 1).join(', ') + ' and ' + words[words.length - 1],
          words: []
        },
        actions: {
          join: (words) => words.length === 1 ? words[0] : words.splice(0, words.length - 1).join(', ') + ' and ' + words[words.length - 1],
          words: []
        }
      },
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
        'An Idle'
      ]
    }
  },
  methods: {
    genGenre () {
      return Sentencer.make(`{{ genres(${this.genres}) }}`)
    },
    makeSentence () {
      // Validation
      this.genres = (this.genres < 1) ? 1 : (this.genres > this.gameGenres.length) ? this.gameGenres.length : this.genres

      this.idea = Sentencer.make(`{{ genres(${this.genres}) }} game about {{ topics(${this.topics}, ${this.fancyTopics}) }} where you must {{ actions(${this.actions}, ${this.fancyActions}) }}.`)
    }
  },
  created () {
    // Pressing the spacebar will generate a new idea
    window.addEventListener('keydown', e => {
      if (e.keyCode === 32) {
        this.makeSentence()
      }
    })

    // Binding this to the vue instance before passing to sentence configuration
    let getGenre = () => {
      return this.gameGenres[Math.floor(Math.random() * this.gameGenres.length)]
    }

    Sentencer.configure({
      actions: {
        verb () {
          return Verbs[Math.floor(Math.random() * Verbs.length)]
        },
        genres (num) {
          if (num === 1) {
            return getGenre()
          } else {
            let result = [getGenre()]
            for (let i = 1; i < num; i++) {
              let genre = getGenre().split(' ').splice(1, 2).join(' ')
              if (!result.includes(genre)) {
                result.push(genre)
              }
            }
            return result.join(' / ')
          }
        },
        topics (num, fancy) {
          let result = []
          for (let i = 0; i < num; i++) {
            result.push(fancy ? `${this.an_adjective()} ${this.noun()}` : this.a_noun())
          }
          return result.length === 1 ? result[0] : result.splice(0, result.length - 1).join(', ') + ' and ' + result[result.length - 1]
        },
        actions (num, fancy) {
          let result = []
          for (let i = 0; i < num; i++) {
            result.push(fancy ? `${this.verb()} ${this.an_adjective()} ${this.noun()}` : `${this.verb()} ${this.a_noun()}`)
          }
          return result.length === 1 ? result[0] : result.splice(0, result.length - 1).join(', ') + ' and ' + result[result.length - 1]
        }
      }
    })

    this.makeSentence() // Load page with a random idea
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
