<template>
  <span>
    <span v-for="word in fragment.words" :key="word.noun">
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
