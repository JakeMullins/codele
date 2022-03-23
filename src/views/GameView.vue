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
            v-bind:input="input"
            @fieldSelected="changeSelected($event)"
          />
        </div>
      </div>
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
        a: "2",
        b: "3",
        0: "print a 1",
        1: "add a 4",
        2: "subtract b 5",
        3: "assign b 5",
        4: "print b 3",
        result: "2 5 5 5",
      },
      input: {
        1: {
          functionString: "print",
          arg1: "1",
          arg2: "2",
        },
        2: {
          functionString: "",
          arg1: "x",
          arg2: "2",
        },
        3: {
          functionString: "subtract",
          arg1: "y",
          arg2: "5",
        },
        4: {
          functionString: "",
          arg1: "",
          arg2: "",
        },
        5: {
          functionString: "set",
          arg1: "x",
          arg2: "2",
        },
        currSelected: -1,
      },
    };
  },
  components: {
    GameRow,
  },
  // Key down event handler
  created() {
    window.addEventListener("keydown", (e) => {
      // If letter
      // Or if backspace
      if (
        e.key.toLowerCase() != e.key.toUpperCase() &&
        (e.key.length == 1 || e.key == "Backspace") 
      ) {
        this.appendToEntry(e.key);
      }
    });
  },
  methods: {
    // Called when a field is clicked
    changeSelected(data) {
      this.input.currSelected = data;
    },
    appendToEntry(input) {
      // Could possibly parse currSelected string to get correct
      let selected = this.$data.input.currSelected;
      let arr = selected.split("-");

      let func = this.$data.input[arr[0]].functionString;
      let arg1 = this.$data.input[arr[0]].arg1;
      let arg2 = this.$data.input[arr[0]].arg2;

      if (arr[1] == "function") {
        if (input == "Backspace") {
          this.$data.input[arr[0]].functionString = func.substring(
            0,
            func.length - 1
          );
        } else {
          this.$data.input[arr[0]].functionString += input;
        }
      }

      if (arr[1] == "arg1") {
        if (input == "Backspace") {
          this.$data.input[arr[0]].arg1 = arg1.substring(0, arg1.length - 1);
        } else {
          this.$data.input[arr[0]].arg1 += input;
        }
      }

      if (arr[1] == "arg2") {
        if (input == "Backspace") {
          this.$data.input[arr[0]].arg2 = arg2.substring(0, arg2.length - 1);
        } else {
          this.$data.input[arr[0]].arg2 += input;
        }
      }

      console.log(func, arg1, arg2);

      //      console.log(this.$data.input[arr[0]]);
      // Add character to entry
      // If backspace, delete one character
    },
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