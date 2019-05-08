<template>
  <div class="hello">
      <h1>{{ msg }}</h1>

      <h2>Options:</h2>
      <div class="options-container">
        <div class="options">
          <span class="option-label">
            <label class="block" for="genres">Genres</label>
            <input v-model="genres" type="number" id="genres">
          </span>

          <span class="option-label">
            <label class="block" for="nouns">Stuffs</label>
            <input v-model="nouns" type="number" id="nouns">
          </span>

          <span class="option-label">
            <label class="block" for="adjectives">Fanciness</label>
            <input v-model="adjectives" type="number" id="adjectives">
          </span>

          <span class="option-label">
            <label class="block" for="verbs">Actions</label>
            <input v-model="verbs" type="number" id="verbs">
          </span>
        </div>
      </div>

      <h2>Game idea:</h2>
      <p>A {{ genres }} game where you {{ verbs }} {{ adjectives }} {{ nouns }}.</p>
  </div>
</template>

<script>
export default {
  name: 'TheGenerator',
  props: {
    msg: String
  },
  data () {
    return {
      genres: 1,
      nouns: 1,
      adjectives: 1,
      verbs: 1
    }
  }
}
</script>

<style scoped>
.options-container {
}

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
