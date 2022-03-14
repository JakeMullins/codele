<template>
  <div class="game">
    <div class="game-container">
      <div id="gameTitle">
        <h1>Codele.js</h1>
      </div>
      <div id="board-container">
        <div id="board" style="width: 700px; height: 420px">
          <!--Dynamically assign row strings based on keyboard inputs-->
          <GameRow
            v-bind:correct="currExpression"
            v-bind:row1="currInput[0]"
            v-bind:row2="currInput[0]"
            v-bind:row3="currInput[0]"
            v-bind:row4="currInput[0]"
            v-bind:row5="currInput[0]"
            v-bind:currSelected="currInput.select"
          />
        </div>
      </div>
      <button>Submit</button>
    </div>
  </div>
</template>

<script>
import GameRow from "@/components/GameRow.vue";

export default {
  name: "GameView",
  data: function () {
    return {
      currExpression: {
        "a": 2,
        "b": 3,
        "0": "print a 1",
        "1": "add a 4",
        "2": "subtract b 5",
        "3": "assign b 5",
        "4": "print b 3",
        result: "2 5 5 5",
      },
      currInput: {
        "0": "GameView 1",
        "1": "",
        "2": "",
        "3": "",
        "4": "",
        "selected": -1,
      }
    };
  },
  components: {
    GameRow,
  },
};
</script>

<style scoped>
  /* 
#game {
  Make button go to right spot
     Might have to mess with containers 
}
     */

#board-container {
  display: flex;
  justify-content: center;
}

#game-row {
  display: grid;
}
</style>