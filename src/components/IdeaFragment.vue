<template>
  <span>
    <span v-for="(word, i) in fragment.words" :key="word.noun">
      <!-- Word separators  -->
      <span v-if="fragment.joiner === '/' && fragment.words.length > 1 && i > 0">/</span>
      <span v-if="fragment.joiner === ',' && fragment.words.length > 1 && i > 0">,</span>
      <span v-if="fragment.joiner === ',' && fragment.words.length > 1 && i === fragment.words.length - 1"> and</span>

      <!-- Fragment words  -->
      <idea-word :word="word.verb" />
      <idea-word :word="word.adj" />
      <idea-word :word="word.noun" />
    </span>
  </span>
</template>

<script>
import IdeaWord from '@/components/IdeaWord'

export default {
  name: 'IdeaFragment',
  props: {
    fragment: Object
  },
  components: {
    IdeaWord
  },
  data () {
    return {}
  },
  methods: {
  }
}
</script>

<style>
</style>
