<template>
  <span @click="lockWord">
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

<style>
</style>
