<template>
  <main id="generator" @click.self="generateIdea">
    <div id="options-container">
      <div id="options">
        <span class="option-label">
          <label class="block" for="genres">Genres</label>
          <input v-model="genres" type="number" id="genres" min="1" :max="genresLength">
        </span>

        <span class="form-group">
          <span class="option-label">
            <label class="block" for="topics">Topics</label>
            <input v-model="topics" type="number" id="topics" min="1" :max="MAX_TOPICS">
          </span>

          <span class="option-label">
            <label class="block" for="fancyTopics">Fancy</label>
            <input v-model="fancyTopics" type="checkbox" id="fancyTopics">
          </span>
        </span>

        <span class="form-group">
          <span class="option-label">
            <label class="block" for="actions">Actions</label>
            <input v-model="actions" type="number" id="actions" min="1" :max="MAX_ACTIONS">
          </span>

          <span class="option-label">
            <label class="block" for="fancyActions">Fancy</label>
            <input v-model="fancyActions" type="checkbox" id="fancyActions">
          </span>
        </span>
      </div>
    </div>

    <div id="idea-container">
      <h1 id="idea">
        <idea-fragment :fragment="idea.genres" />
          game about
          <idea-fragment :fragment="idea.topics" />
            where you must
            <idea-fragment :fragment="idea.actions" />
      </h1>
    </div>
    <p id="alt"><em>Press space or tap anywhere for new ideas</em></p>
  </main>
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
        e.preventDefault()
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
        }
      }
    })

    this.generateIdea() // Load page with a random idea
  }
}
</script>

<style scoped>
#generator {
  display: flex;
  position: relative;
  padding: 16px;
  padding-top: 32px;
  flex-direction: column;
  justify-content: space-between;
  height: 93vh;
}

#options-container {
  align-self: flex-end;
}

@media only screen and (max-width: 768px) {
  #options-container {
    align-self: center;
  }
}

#options {
  display: flex;
}

input[type=number] {
  border: none;
  width: 45px;
  border-bottom: 1px solid #D1C3B4;
  background: none;
  outline-color: #ED9B40;
}

input[type=checkbox] {
  transform: scale(1.5);
  margin-top: 8px;
}

.form-group {
  display: flex;
  margin-left: 8px;
  margin-top: -8px;
  border: 1px solid #ED9B40;
  border-radius: 2px;
}

.form-group > .option-label:first-child {
  margin: 8px;
}

.form-group > .option-label:last-child {
  margin-top: 8px;
  margin-right: 8px;
}

.block {
  display: block
}

#idea-container {
  text-align: center;
  margin-bottom: 25vh;
}

#alt {
  align-self: center;
  opacity: 0.8;
  margin-bottom: 48px;
}
</style>
