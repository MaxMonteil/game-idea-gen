<template>
  <span @click="locked = !locked">
    <slot></slot>
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
      locked: false
    }
  }
}
</script>

<style>

</style>
