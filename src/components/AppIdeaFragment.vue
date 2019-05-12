<template>
  <span @click="lockWord">
    {{ displayWord }}
  </span>
</template>

<script>
export default {
  name: 'AppIdeaFragment',
  props: {
    word: String
  },
  data () {
    return {
      cachedWord: '',
      locked: false
    }
  },
  computed: {
    displayWord () {
      if (this.locked) {
        return this.cachedWord
      }
      return this.word
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
  }
}
</script>

<style>

</style>
