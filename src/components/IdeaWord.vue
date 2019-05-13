<template>
  <span class="idea-word" :class="{ visible: word }">
    <span @click="lockWord" class="display-word">
      {{ displayWord }}
    </span>
    <svg
      v-if="word && locked"
      aria-hidden="true"
      focusable="false"
      data-prefix="fas"
      data-icon="lock"
      class="svg-inline--fa fa-lock fa-w-14"
      role="img"
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 448 512"
      width="10"
    >
      <path
        fill="currentColor"
        d="M400 224h-24v-72C376 68.2 307.8 0 224 0S72 68.2 72 152v72H48c-26.5 0-48 21.5-48 48v192c0 26.5 21.5 48 48 48h352c26.5 0 48-21.5 48-48V272c0-26.5-21.5-48-48-48zm-104 0H152v-72c0-39.7 32.3-72 72-72s72 32.3 72 72v72z"
      ></path>
    </svg>
  </span>
</template>

<script>
export default {
  name: 'IdeaWord',
  props: {
    word: String
  },
  data () {
    return {
      displayWord: this.word,
      cachedWord: '',
      locked: false
    }
  },
  methods: {
    lockWord () {
      // Locking word
      if (!this.locked) {
        this.cachedWord = this.word
        this.locked = true
      } else { // Unlocking word
        this.locked = false
      }
    }
  },
  watch: {
    word (newWord) {
      console.log('hit')
      if (this.locked) {
        this.displayWord = this.cachedWord
      } else {
        this.displayWord = newWord
      }
    }
  }
}
</script>

<style scoped>
.idea-word {
  display: inline-flex;
  flex-direction: column;
  align-items: center;
}

.visible {
  padding: 0 0.1em;
}
</style>
