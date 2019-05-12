<template>
  <span @click="lockFrag">
    {{ displayFrag }}
  </span>
</template>

<script>
export default {
  name: 'IdeaFragment',
  props: {
    fragment: String
  },
  data () {
    return {
      displayFrag: this.fragment,
      cachedFrag: '',
      locked: false
    }
  },
  methods: {
    lockFrag () {
      // Locking word
      if (!this.locked) {
        this.cachedFrag = this.fragment
        this.locked = true
      } else { // Unlocking word
        this.locked = false
      }
    }
  },
  watch: {
    fragment (newFrag) {
      if (this.locked) {
        this.displayFrag = this.cachedFrag
      } else {
        this.displayFrag = newFrag
      }
    }
  }
}
</script>

<style>
</style>
