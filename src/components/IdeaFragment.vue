<template>
  <span>
    <span v-for="(word, i) in fragment.words" :key="i">
      <!-- Word separators  -->
      <span v-if="fragment.joiner === '/' && fragment.words.length > 1 && i > 0">/</span>
      <span v-if="fragment.joiner === ',' && fragment.words.length > 1 && i > 0">,</span>
      <span v-if="fragment.joiner === ',' && fragment.words.length > 1 && i === fragment.words.length - 1"> and </span>

      <!-- Fragment words  -->
      <idea-word v-if="word.verb" :word="word.verb" />
      <idea-word v-if="word.adj" :word="word.adj" />
      <idea-word v-if="word.noun" :word="word.noun" />
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
  }
}
</script>

<style>
</style>
