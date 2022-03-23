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
            :rowId="1"
            v-bind:correct="currExpression"
            v-bind:input="input"
            @fieldSelected="changeSelected($event)"
            @guessSubmitted="guessSubmitted()"
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
      rows: [1, 2, 3, 4, 5],
      currExpression: {
        x: "2",
        y: "3",
        z: "4",
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
        currSelectedField: -1,
        currSelectedRow: 1,
      },
      fieldStates: {
        1: {
          func: "function-unselected",
          arg1: "argument-unselected",
          arg2: "argument-unselected"
        },
        2: {
          func: "function-unselected",
          arg1: "argument-unselected",
          arg2: "argument-unselected"
        },
        3: {
          func: "function-unselected",
          arg1: "argument-unselected",
          arg2: "argument-unselected"
        },
        4: {
          func: "function-unselected",
          arg1: "argument-unselected",
          arg2: "argument-unselected"
        },
        5: {
          func: "function-unselected",
          arg1: "argument-unselected",
          arg2: "argument-unselected"
        } ,
      }
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
      this.input.currSelectedField = data;
    },
    appendToEntry(input) {
      // Could possibly parse currSelected string to get correct
      let selected = this.$data.input.currSelectedField;
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
      // Add character to entry
      // If backspace, delete one character
    },
    guessSubmitted() {
      // Reset selection and advance rows
      this.input.currSelectedRow++;
      this.input.currSelectedField = -1;
      this.checkGuess();
    },
    checkGuess() {
      let guessRows = [1, 2, 3, 4, 5];
      guessRows.forEach((row) => {
        this.checkFunction(row, this.input[row].functionString);
        this.checkArg1(row, this.input[row].arg1);
        this.checkArg2(row, this.input[row].arg2);
      });

      // For each guessRow
      // Check function and assign color
      // Check arg1 and assign color
      // Check arg2 and assign color
    },
    checkFunction(row, string) {
      console.log(row, string);
    },
    checkArg1(row, string) {
      console.log(row, string);
    },
    checkArg2(row, string) {
      console.log(row, string);
    }
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