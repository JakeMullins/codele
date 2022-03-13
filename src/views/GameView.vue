<template>
  <div class="game">
    <div id="gameTitle">
      <h1>Codele.js</h1>
    </div>
    <div id="board-container">
      <div id="board" style="width: 700px; height: 420px">
        <GameRow v-bind:yellow="One" v-bind:green="[4, 5, 6]" />
        <GameRow v-bind:yellow="Two" v-bind:green="[4, 5, 6]" />
        <GameRow v-bind:yellow="Three" v-bind:green="[4, 5, 6]" />

      </div>
    </div>
  </div>
</template>

<script>
import GameRow from "@/components/GameRow.vue";

export default {
  name: "GameView",
  el: "#app",
  data: function () {
    return {
      yellowString: "Poggers",
    };
  },
  components: {
    GameRow,
  },
};
</script>

<style scoped>
#board-container {
  display: flex;
  justify-content: center;
}

#game-row {
  display: grid;
}
</style>