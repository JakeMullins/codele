<template>
  <div class="game">
    <div class="game-container">
      <div id="gameTitle">
        <h1>Codele.js</h1>
      </div>
      <div id="board-container">
        <div id="documentation"></div>
        <div id="board" style="width: 700px; height: 420px">
          <!--Dynamically assign row strings based on keyboard inputs-->
          <DocsPanel 
            v-bind:toggled="helpToggled"
          />
          <GameRow
            :rowId="1"
            v-bind:correct="currExpression"
            v-bind:input="input"
            v-bind:fieldStates="fieldStates"
            v-bind:interpretedString="result"
            @fieldSelected="changeSelected($event)"
            @guessSubmitted="guessSubmitted(1)"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

import GameRow from "@/components/GameRow.vue";
import DocsPanel from "@/components/DocsPanel.vue";

export default {
  name: "GameView",
  data: function () {
    return {
      helpToggled: true,
      rows: [1, 2, 3, 4, 5],
      currExpression: {
        '1': { functionString: 'print', arg1: 'x', arg2: 2 },
        '2': { functionString: 'add', arg1: 'x', arg2: 'z' },
        '3': { functionString: 'subtract', arg1: 'y', arg2: 2 },
        '4': { functionString: 'set', arg1: 'x', arg2: 3 },
        '5': { functionString: 'print', arg1: 'y', arg2: 2 },
        // dynamic vs static 
        x: 2,
        y: 3,
        z: 4,
        functionList: [ 'print', 'add', 'subtract', 'set' ],
        arg1List: [ '1', 'x', 'y' ],
        arg2List: [ '2', '5', '4' ],
        result: '2 555'
      },
      input: {
        static_x: 2,
        x: 2,
        static_y: 3,
        y: 3,
        static_z: 4,
        z: 4,
        1: {
          functionString: "",
          arg1: "",
          arg2: ""
        },
        2: {
          functionString: "",
          arg1: "",
          arg2: ""
        },
        3: {
          functionString: "",
          arg1: "",
          arg2: ""
        },
        4: {
          functionString: "",
          arg1: "",
          arg2: ""
        },
        5: {
          functionString: "",
          arg1: "",
          arg2: ""
        },
        currSelectedField: -1,
        currSelectedRow: 1
      },
      defaultStates: {
        1: {
          function: "function-unselected",
          arg1: "argument-unselected",
          arg2: "argument-unselected"
        },
        2: {
          function: "function-unselected",
          arg1: "argument-unselected",
          arg2: "argument-unselected"
        },
        3: {
          function: "function-unselected",
          arg1: "argument-unselected",
          arg2: "argument-unselected"
        },
        4: {
          function: "function-unselected",
          arg1: "argument-unselected",
          arg2: "argument-unselected"
        },
        5: {
          function: "function-unselected",
          arg1: "argument-unselected",
          arg2: "argument-unselected"
        }
      },
      fieldStates: {
        1: {
          function: "function-unselected",
          arg1: "argument-unselected",
          arg2: "argument-unselected"
        },
        2: {
          function: "function-unselected",
          arg1: "argument-unselected",
          arg2: "argument-unselected"
        },
        3: {
          function: "function-unselected",
          arg1: "argument-unselected",
          arg2: "argument-unselected"
        },
        4: {
          function: "function-unselected",
          arg1: "argument-unselected",
          arg2: "argument-unselected"
        },
        5: {
          function: "function-unselected",
          arg1: "argument-unselected",
          arg2: "argument-unselected"
        }
      },
      possibleFunctionStrings: [
        "print",
        "add",
        "subtract",
        "divide",
        "multiply",
        "assign"
      ],
      possibleArg1String: ["x", "y", "z"],
      possibleArg2String: [
        "x",
        "y",
        "z",
        "0",
        "1",
        "2",
        "3",
        "4",
        "5",
        "6",
        "7",
        "8",
        "9",
        "10",
        "11",
        "12",
        "13",
        "14",
        "15"
      ],
      result: ""
    };
  },
  components: {
    GameRow,
    DocsPanel
  },
  // Key down event handler
  created() {
    window.addEventListener("keydown", (e) => {
      // Add possible unselected short circuit

      // If letter
      // Or if backspace
      if (
        e.key.toLowerCase() != e.key.toUpperCase() &&
        (e.key.length == 1 || e.key == "Backspace")
      ) {
        this.appendToEntry(e.key);
      }
      // If number
      if (!isNaN(e.key)) {
        this.appendToEntry(e.key);
      }
    });
  
    this.getExpression();
  },
  methods: {
    async getExpression(){
      try{
        console.log("Attempting connection")
        let response = await axios.get('http://localhost:3000/api/expression');
        console.log(response);
        this.currExpression = response.data;
        return true;
      } catch(e) {
        console.log(e);
      }
    },
    // Called when a field is clicked
    changeSelected(field) {
      this.input.currSelectedField = field;
      let arr = this.input.currSelectedField.split("-");
      let className = "";
      if (arr[1] == "function") {
        className = "function-selected";
      } else {
        className = "argument-selected";
      }

      // Iterate through all fieldStates and change to function/argument-unselected
      for (const row in this.fieldStates) {
        for (const entry in this.fieldStates[row]) {
          if (entry == "function") {
            this.fieldStates[row][entry] = "function-unselected";
          }
          if (entry == "arg1" || entry == "arg2") {
            this.fieldStates[row][entry] = "argument-unselected";
          }
        }
      }

      this.fieldStates[arr[0]][arr[1]] = className;
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
    guessSubmitted(id) {
      this.input.currSelectedField = id;
      this.input.currSelectedField = -1;
      this.checkGuess();
    },
    checkGuess() {
      this.changeAllFieldsUnselected();

      let guessRows = [1, 2, 3, 4, 5];

      // Change field colors
      guessRows.forEach((row) => {
        this.checkFunction(row, this.input[row].functionString);
        this.checkArg1(row, this.input[row].arg1);
        this.checkArg2(row, this.input[row].arg2);
      });

      // Run interpreter
      this.result = this.interpret();
    },
    checkFunction(row, inputString) {
      // Gray
      // Valid syntax
      if (
        this.possibleFunctionStrings.includes(this.input[row].functionString)
      ) {
        this.fieldStates[row].function = "function-unselected";
      }
      // Red
      else {
        this.fieldStates[row].function = "function-invalid-syntax";
      }

      // Yellow
      // Check if inputString is in correct, but NOT in the same spot
      if (
        this.currExpression.functionList.includes(
          this.input[row].functionString
        )
      ) {
        // Change this.fieldStates[row].function = "function-different-spot"
        this.fieldStates[row].function = "function-different-spot";
      }

      // Green
      // Check if inputString is same as correct
      if (this.currExpression[row].functionString === inputString) {
        // Change this.fieldStates[row].function = "function-correct"
        this.fieldStates[row].function = "function-correct";
      }

      // Check if inputString is not a valid entry
      // Change this.fieldStates[row].function = "function-invalid-syntax"

      // Check if valid syntax but not in correct
      // Change this.fieldStates[row].function = "function-unselected"
    },
    checkArg1(row, inputString) {

      let varRegEx = /x|y|z/;
      // Gray
      if(inputString.match(varRegEx)){
        this.fieldStates[row].arg1 = "argument-unselected";
      } else {
        // Red
        this.fieldStates[row].arg1 = "argument-invalid-syntax";
        return;
      }

      // Yellow
      if(this.currExpression.arg1List.includes(inputString)) {
        this.fieldStates[row].arg1 = "argument-different-spot";
      }

      // Green
      if (this.currExpression[row].arg1 == inputString) {
        this.fieldStates[row].arg1 = "argument-correct"; 
      }
    },

    checkArg2(row, inputString) {

      let notNumberRegEx = /[a-z]/;
      let numberRegEx = /\d+/;

      // Gray 
      if(!inputString.match(notNumberRegEx) && inputString.match(numberRegEx)){
        this.fieldStates[row].arg2 = "argument-unselected";
      } else {
        // Red
        this.fieldStates[row].arg2 = "argument-invalid-syntax";
        return;
      }

      // Yellow
      if(this.currExpression.arg2List.includes(inputString)){
        this.fieldStates[row].arg2 = "argument-different-spot";
      }

      // Green
      if(this.currExpression[row].arg2 == inputString){
        this.fieldStates[row].arg2 = "argument-correct";
      }
    },
    changeAllFieldsUnselected() {
      for (const row in this.fieldStates) {
        for (const entry in this.fieldStates[row]) {
          if (entry == "function") {
            this.fieldStates[row][entry] = "function-unselected";
          }
          if (entry == "arg1" || entry == "arg2") {
            this.fieldStates[row][entry] = "argument-unselected";
          }
        }
      }
    },
    // Called in checkGuess
    interpret() {
      let result = "";

      this.rows.forEach((row) => {
        // let arg1 = this.input[row].arg1;
        let arg2 = this.input[row].arg2;
        // let func = this.input[row].functionString;

        // let arg1IsNumber = arg1 == "x" || arg1 == "y" || arg1 == "z";
        let arg2IsNumber = arg2 == "x" || arg2 == "y" || arg2 == "z";

        // 'Execute' each function
        switch (this.input[row].functionString) {
          case "print":
            for (let i = 0; i < this.input[row].arg2; i++) {
              // Append to result
              result += this.input[this.input[row].arg1];
            }
            result += " ";
            break;
          case "add":
            if (arg2IsNumber) {
              this.input[this.input[row].arg1] +=
                this.input[this.input[row].arg2];
            } else {
              this.input[this.input[row].arg1] += this.input[row].arg2;
            }
            break;
          case "subtract":
            if (arg2IsNumber) {
              this.input[this.input[row].arg1] -=
                this.input[this.input[row].arg2];
            } else {
              this.input[this.input[row].arg1] -= this.input[row].arg2;
            }
            break;
          case "multiply":
            if (arg2IsNumber) {
              this.input[this.input[row].arg1] *=
                this.input[this.input[row].arg2];
            } else {
              this.input[this.input[row].arg1] *= this.input[row].arg2;
            }
            break;
          case "divide":
            if (arg2IsNumber) {
              this.input[this.input[row].arg1] /=
                this.input[this.input[row].arg2];
            } else {
              this.input[this.input[row].arg1] /= this.input[row].arg2;
            }
            break;
          case "set":
            this.input[this.input[row].arg1] = this.input[row].arg2;
            break;
          default:
            console.log("default");
        }

        this.input.x = this.input.static_x;
        this.input.y = this.input.static_y;
        this.input.z = this.input.static_z;
      });

      return result;
    }
  }
};
</script>

<style scoped>
#board-container {
  display: flex;
  justify-content: center;
}

#game-container{ 
  max-width: 50vw;
}

#game-row {
  display: grid;
}
</style>
