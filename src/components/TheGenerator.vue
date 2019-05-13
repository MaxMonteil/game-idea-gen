<template>
  <div>
      <h1>Game Idea Generator</h1>

      <h2>Options:</h2>
      <div class="options-container">
        <div class="options">
          <span class="option-label">
            <label class="block" for="genres">Genres</label>
            <input v-model="genres" type="number" id="genres" min="1" :max="genresLength">
          </span>

          <span class="option-label">
            <label class="block" for="fancyTopics">Fancy?</label>
            <input v-model="fancyTopics" type="checkbox" id="fancyTopics">
          </span>

          <span class="option-label">
            <label class="block" for="topics">Topics</label>
            <input v-model="topics" type="number" id="topics" min="1" :max="MAX_TOPICS">
          </span>

          <span class="option-label">
            <label class="block" for="fancyActions">Fancy?</label>
            <input v-model="fancyActions" type="checkbox" id="fancyActions">
          </span>

          <span class="option-label">
            <label class="block" for="actions">Actions</label>
            <input v-model="actions" type="number" id="actions" min="1" :max="MAX_ACTIONS">
          </span>
        </div>
      </div>

      <h2>Game idea:</h2>
      <p class="idea">
        <idea-fragment :fragment="idea.genres" /> game about <idea-fragment :fragment="idea.topics" /> where you must <idea-fragment :fragment="idea.actions" />
      </p>
      <button @click="generateIdea">Generate!</button>
  </div>
</template>

<script>
import Verbs from '@/assets/verbs.js'
import { Genres } from '@/assets/genres.js'
import Sentencer from 'sentencer'

import IdeaFragment from '@/components/IdeaFragment'

export default {
  name: 'TheGenerator',
  components: {
    IdeaFragment
  },
  data () {
    return {
      genresLength: Genres.length,
      genres: 1,
      fancyTopics: true,
      topics: 1,
      MAX_TOPICS: 10,
      fancyActions: true,
      actions: 1,
      MAX_ACTIONS: 10,
      idea: {
        genres: {
          joiner: '/',
          words: []
        },
        topics: {
          joiner: ',',
          words: []
        },
        actions: {
          joiner: ',',
          words: []
        }
      }
    }
  },
  methods: {
    resetData () {
      this.idea.genres.words = []
      this.idea.topics.words = []
      this.idea.actions.words = []
    },
    generateIdea () {
      this.resetData()

      // Validation
      this.genres = (this.genres < 1) ? 1 : (this.genres > Genres.length) ? Genres.length : this.genres
      this.topics = (this.topics < 1) ? 1 : (this.topics > this.MAX_TOPICS) ? this.MAX_TOPICS : this.topics
      this.actions = (this.actions < 1) ? 1 : (this.actions > this.MAX_ACTIONS) ? this.MAX_ACTIONS : this.actions

      // Generation
      this.idea.genres.words.push({ noun: Sentencer.make('{{ a_genre }}'), adj: '', verb: '' })
      for (let i = 0; i < this.genres - 1; i++) {
        let genre = Sentencer.make('{{ genre }}')
        if (!this.idea.genres.words.map(obj => obj.noun).includes(genre)) {
          this.idea.genres.words.push({ noun: genre, adj: '', verb: '' })
        }
      }

      if (this.fancyTopics) {
        for (let i = 0; i < this.topics; i++) {
          this.idea.topics.words.push({ noun: Sentencer.make('{{ noun }}'), adj: Sentencer.make('{{ an_adjective }}'), verb: '' })
        }
      } else {
        for (let i = 0; i < this.topics; i++) {
          this.idea.topics.words.push({ noun: Sentencer.make('{{ a_noun }}'), adj: '', verb: '' })
        }
      }

      if (this.fancyActions) {
        for (let i = 0; i < this.actions; i++) {
          this.idea.actions.words.push({ noun: Sentencer.make('{{ noun }}'), adj: Sentencer.make('{{ an_adjective }}'), verb: Sentencer.make('{{ verb }}') })
        }
      } else {
        for (let i = 0; i < this.actions; i++) {
          this.idea.actions.words.push({ noun: Sentencer.make('{{ a_noun }}'), adj: '', verb: Sentencer.make('{{ verb }}') })
        }
      }
    }
  },
  created () {
    // Pressing the spacebar will generate a new idea
    window.addEventListener('keydown', e => {
      if (e.keyCode === 32) {
        this.generateIdea()
      }
    })

    // Binding this to the vue instance before passing to sentence configuration
    let getGenre = () => {
      return Genres[Math.floor(Math.random() * Genres.length)]
    }

    Sentencer.configure({
      actions: {
        verb () {
          return Verbs[Math.floor(Math.random() * Verbs.length)]
        },
        genre () {
          return getGenre().split(' ').splice(1, 2).join(' ')
        },
        a_genre () {
          return getGenre()
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

    this.generateIdea() // Load page with a random idea
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

.idea {
  user-select: none;
}
</style>
