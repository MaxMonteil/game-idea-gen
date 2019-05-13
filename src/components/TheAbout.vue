<template>
  <article id="about">
    <h2>What's this?</h2>
    <p>Welcome to a totally random game idea generator!</p>
    <p>The premise is simple, keep generating new ideas untils you find an idea you love. Most of them won't make sense, what you can do is lock the words you like and let the rest of the sentence continue changing.</p>
    <p>There are also some other settings you can play around with like the number of game genres, topics, or actions. Making things fancy will also generate adjectives.</p>

    <h2>How does it work?</h2>
    <p>I'm using <a href="http://kylestetz.github.io/Sentencer/">Sentencer</a> to generate random nouns and adjectives plus my own list of verbs and game genres.</p>
    <p>You can check the full lists and the site code over on Github.</p>
  </article>
</template>

<script>
export default {

}
</script>

<style scoped>
#about {
  padding: 64px 25vw;
  background-color: #FFF;
  color: #161616;
}

@media only screen and (max-width: 768px) {
  #about {
  padding: 64px 10vw;
  }
}

h2 {
  font-size: 2em;
}
</style>
