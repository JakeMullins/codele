<template>
  <div class="guess">
    <div class="initialConditions">
      <div class="initialCondition" id="cond1">
        <h1 class="label">x:</h1>
        <div class="initialValue">{{ correct.x }}</div>
      </div>
      <div class="initialCondition" id="cond2">
        <h1 class="label">y:</h1>
        <div class="initialValue">{{ correct.y }}</div>
      </div>
      <div class="initialCondition" id="cond3">
        <h1 class="label">z:</h1>
        <div class="initialValue">{{ correct.z }}</div>
      </div>
    </div>
    <div class="row" id="row1">
      <div
        v-bind:class="this.$props.fieldStates[1].function"
        id="1-function"
        @click="fieldSelect('1-function')"
      >
        {{ input[1].functionString }}
      </div>
      <div
        v-bind:class="this.$props.fieldStates[1].arg1"
        id="1-arg1"
        @click="fieldSelect('1-arg1')"
      >
        {{ input[1].arg1 }}
      </div>
      <div
        v-bind:class="this.$props.fieldStates[1].arg2"
        id="1-arg2"
        @click="fieldSelect('1-arg2')"
      >
        {{ input[1].arg2 }}
      </div>
    </div>
    <div class="row" id="row2">
      <div
        v-bind:class="this.$props.fieldStates[2].function"
        id="2-function"
        @click="fieldSelect('2-function')"
      >
        {{ input[2].functionString }}
      </div>
      <div
        v-bind:class="this.$props.fieldStates[2].arg1"
        id="2-arg1"
        @click="fieldSelect('2-arg1')"
      >
        {{ input[2].arg1 }}
      </div>
      <div
        v-bind:class="this.$props.fieldStates[2].arg2"
        id="2-arg2"
        @click="fieldSelect('2-arg2')"
      >
        {{ input[2].arg2 }}
      </div>
    </div>
    <div class="row" id="row3">
      <div
        v-bind:class="this.$props.fieldStates[3].function"
        @click="fieldSelect('3-function')"
      >
        {{ input[3].functionString }}
      </div>
      <div
        v-bind:class="this.$props.fieldStates[3].arg1"
        id="3-arg1"
        @click="fieldSelect('3-arg1')"
      >
        {{ input[3].arg1 }}
      </div>
      <div
        v-bind:class="this.$props.fieldStates[3].arg2"
        id="3-arg2"
        @click="fieldSelect('3-arg2')"
      >
        {{ input[3].arg2 }}
      </div>
    </div>
    <div class="row" id="row4">
      <div
        v-bind:class="this.$props.fieldStates[4].function"
        id="4-function"
        @click="fieldSelect('4-function')"
      >
        {{ input[4].functionString }}
      </div>
      <div
        v-bind:class="this.$props.fieldStates[4].arg1"
        id="4-arg1"
        @click="fieldSelect('4-arg1')"
      >
        {{ input[4].arg1 }}
      </div>
      <div
        v-bind:class="this.$props.fieldStates[4].arg2"
        id="4-arg2"
        @click="fieldSelect('4-arg2')"
      >
        {{ input[4].arg2 }}
      </div>
    </div>
    <div class="row" id="row5">
      <div
        v-bind:class="this.$props.fieldStates[5].function"
        id="5-function"
        @click="fieldSelect('5-function')"
      >
        {{ input[5].functionString }}
      </div>
      <div
        v-bind:class="this.$props.fieldStates[5].arg1"
        id="5-arg1"
        @click="fieldSelect('5-arg1')"
      >
        {{ input[5].arg1 }}
      </div>
      <div
        v-bind:class="this.$props.fieldStates[5].arg2"
        id="5-arg2"
        @click="fieldSelect('5-arg2')"
      >
        {{ input[5].arg2 }}
      </div>
    </div>
    <div class="end">
      <button class="button-unpressed" id="button" @click="submitGuess()">
        Submit
      </button>
     <div class="result" id="user">{{ interpretedString }}</div>
     <div class="result" id="answer">{{ correct.result }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "GameRow",
  created() {
    console.log(this.$props.correct);
  },
  // Put data here
  props: {
    correct: Object,
    input: Object,
    rowId: Number,
    interpretedString: String,
    fieldStates: Object
  },
  methods: {
    // Sets current ID =
    testEvent() {
      this.$emit("testEvent");
    },
    fieldSelect(field) {
      if (this.$props.rowId == this.$props.input.currSelectedRow) {
        this.currentId = field;
        // Emit the row and whether it is a func or 1 of 2 arg
        this.$emit("fieldSelected", this.currentId);
      }
    },
    submitGuess() {
      if (this.$props.input.currSelectedRow == this.$props.rowId) {
        this.$emit("guessSubmitted");
      }
    }
  },
  data: function () {
    return {
      currentId: "No field selected",
      fieldIDs: [
        "1-function",
        "1-arg1",
        "1-arg2",
        "2-function",
        "2-arg1",
        "2-arg2",
        "3-function",
        "3-arg1",
        "3-arg2",
        "4-function",
        "4-arg1",
        "4-arg2",
        "5-function",
        "5-arg1",
        "5-arg2"
      ],
      functionIDs: [
        "1-function",
        "2-function",
        "3-function",
        "4-function",
        "5-function"
      ],
      argumentIDs: [
        "1-arg1",
        "1-arg2",
        "2-arg1",
        "2-arg2",
        "3-arg1",
        "3-arg2",
        "4-arg1",
        "4-arg2",
        "5-arg1",
        "5-arg2"
      ]
    };
  }
};
</script>

<style scoped>
p {
  padding: 0px;
  margin: 0px;
}

.button-unpressed {
  display: inline-block;
  width: 280px;
  height: 100px;
  background-color: #2b2b2b;
  color: #fff;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}

.button-pressed {
  display: inline-block;
  width: 280px;
  height: 100px;
  background-color: #5b5b5b;
  color: #fff;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}

.initialConditions {
  display: flex;
  justify-content: center;
  vertical-align: center;
}

.initialCondition {
  display: flex;
  justify-content: center;
}

.label {
  display: inline-block;
  color: #fff;
  margin: 5px;
  font-size: 60px;
  vertical-align: middle;
}

.initialValue {
  padding: 5px 0px 0px 0px;
  display: inline-block;
  width: 85px;
  height: 85px;
  background-color: #2b2b2b;
  color: #fff;
  margin: 5px;
  font-size: 60px;
  vertical-align: middle;
}

.row {
  box-sizing: border-box;
  text-align: center;
  vertical-align: center;
}

.end {
  display: box;
}

.result {
  display: inline-block;
  width: 520px;
  height: 80px;
  background-color: #2b2b2b;
  color: #fff;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle; 
}

.function-unselected {
  display: inline-block;
  width: 300px;
  height: 90px;
  background-color: #2b2b2b;
  color: #fff;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}

.function-selected {
  display: inline-block;
  width: 300px;
  height: 90px;
  background-color: #fff;
  color: #2b2b2b;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}

.function-correct {
  display: inline-block;
  width: 300px;
  height: 90px;
  background-color: #538d4e;
  color: #2b2b2b;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}

.function-different-spot {
  display: inline-block;
  width: 300px;
  height: 90px;
  background-color: #b59f3b;
  color: #2b2b2b;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}

.function-invalid-syntax {
  display: inline-block;
  width: 300px;
  height: 90px;
  background-color: #f44646;
  color: #2b2b2b;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}

.argument-unselected {
  display: inline-block;
  width: 100px;
  height: 90px;
  background-color: #2b2b2b;
  color: #fff;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}

.argument-selected {
  display: inline-block;
  width: 100px;
  height: 90px;
  background-color: #fff;
  color: #2b2b2b;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}

.argument-correct {
  display: inline-block;
  width: 100px;
  height: 90px;
  background-color: #538d4e;
  color: #2b2b2b;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}

.argument-different-spot {
  display: inline-block;
  width: 100px;
  height: 90px;
  background-color: #b59f3b;
  color: #2b2b2b;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}

.argument-invalid-syntax {
  display: inline-block;
  width: 100px;
  height: 90px;
  background-color: #f44646;
  color: #2b2b2b;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}
</style>
