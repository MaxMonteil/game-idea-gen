<template>
  <article id="about">
    <h2>What's this?</h2>
    <p>Welcome to a totally random game idea generator!</p>
    <p>The premise is simple, keep generating new ideas untils you find an idea you love. Most of them won't make sense, what you can do is lock the words you like and let the rest of the sentence continue changing.</p>
    <p>There are also some other settings you can play around with like the number of game genres, topics, or actions. Making things fancy will also generate adjectives.</p>

    <h2>How does it work?</h2>
    <p>I'm using <a href="http://kylestetz.github.io/Sentencer/">Sentencer</a> to generate random nouns and adjectives plus my own list of verbs and game genres.</p>
    <p>You can check the full lists and the site code over on <a href="https://github.com/MaxMonteil/game-idea-gen">Github</a>.</p>

    <h2>Available Genres</h2>
    <p>List of genres taken from <a href="https://en.wikipedia.org/wiki/List_of_video_game_genres">Wikipedia</a>.</p>
    <ul>
      <li>Platformer</li>
      <li>Shooter</li>
      <li>Fighting</li>
      <li>Beat 'em up</li>
      <li>Stealth</li>
      <li>Survival</li>
      <li>Rhythm</li>
      <li>Survival horror</li>
      <li>Metroidvania</li>
      <li>Text adventure</li>
      <li>Graphic adventure</li>
      <li>Visual novel</li>
      <li>Interactive movie</li>
      <li>Real-time 3D adventure</li>
      <li>Action RPG</li>
      <li>MMORPG</li>
      <li>Roguelike</li>
      <li>Tactical RPG</li>
      <li>Sandbox RPG</li>
      <li>First-person party-based RPG</li>
      <li>Choices</li>
      <li>Fantasy</li>
      <li>Construction and management simulation</li>
      <li>Life simulation</li>
      <li>Vehicle simulation</li>
      <li>4X</li>
      <li>Artillery</li>
      <li>Real-time strategy (RTS)</li>
      <li>Real-time tactics (RTT)</li>
      <li>Multiplayer online battle arena (MOBA)</li>
      <li>Tower defense</li>
      <li>Turn-based strategy (TBS)</li>
      <li>Turn-based tactics (TBT)</li>
      <li>Wargame</li>
      <li>Racing</li>
      <li>Sports</li>
      <li>Sports-based fighting</li>
      <li>MMO</li>
      <li>Casual</li>
      <li>Party</li>
      <li>Programming</li>
      <li>Logic</li>
      <li>Trivia</li>
      <li>Board</li>
      <li>Card</li>
      <li>Idle</li>
    </ul>

    <h2>Numbers</h2>
    <table>
      <thead>
        <tr>
          <th>Word List</th>
          <th>Size</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Game Genres</td>
          <td>46</td>
        </tr>
        <tr>
          <td>Nouns</td>
          <td>2273</td>
        </tr>
        <tr>
          <td>Adjectives</td>
          <td>5176</td>
        </tr>
        <tr>
          <td>Verbs</td>
          <td>9860</td>
        </tr>
      </tbody>
    </table>

    <h2>Contributing</h2>
    <p>As you've noticed most of the ideas might not really make sense, feel free to make suggestions about words that should be removed or added to either list. Same for ideas about some extra features, let me know on <a href="https://github.com/MaxMonteil/game-idea-gen">Github</a>.</p>
  </article>
</template>

<script>
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

a {
  color: #ED9B40;
}

a:visited {
  color: #825523;
}

table {
  text-align: left;
  border-spacing: 24px 8px;
}
</style>
