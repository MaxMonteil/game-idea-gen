<template>
  <span @click="lockWord" :class="{ locked: locked }" class="display-word">
    {{ displayWord }}
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
.locked {
  opacity: 0.5;
}

.display-word {
  text-decoration: underline;
}

.display-word:hover {
  opacity: 0.5;
}
</style>
