<template>
  <div class="guess">
    <div class="row" id="row1">
      <div v-bind:class="[this.currentId==='1-function'?'function-selected':'function-unselected']" id="1-function" @click="fieldSelect('1-function')">
        {{ input[1].functionString }}
      </div>
      <div v-bind:class="[ (this.currentId === '1-arg1') ? 'argument-selected' : 'argument-unselected' ]" id="1-arg1" @click="fieldSelect('1-arg1')">
        {{ input[1].arg1 }}
      </div>
      <div v-bind:class="[ (this.currentId === '1-arg2') ? 'argument-selected' : 'argument-unselected' ]" id="1-arg2" @click="fieldSelect('1-arg2')">
        {{ input[1].arg2 }}
      </div>
    </div>
    <div class="row" id="row2">
      <div v-bind:class="[this.currentId==='2-function'?'function-selected':'function-unselected']" id="2-function" @click="fieldSelect('2-function')">
        {{ input[2].functionString }}
      </div>
      <div v-bind:class="[ (this.currentId === '2-arg1') ? 'argument-selected' : 'argument-unselected' ]" id="2-arg1" @click="fieldSelect('2-arg1')">
        {{ input[2].arg1 }}
      </div>
      <div v-bind:class="[ (this.currentId === '2-arg2') ? 'argument-selected' : 'argument-unselected' ]" id="2-arg2" @click="fieldSelect('2-arg2')">
        {{ input[2].arg2 }}
      </div>
    </div>
    <div class="row" id="row3">
      <div v-bind:class="[this.currentId==='3-function'?'function-selected':'function-unselected']" id="3-function" @click="fieldSelect('3-function')">
        {{ input[3].functionString }}
      </div>
      <div v-bind:class="[ (this.currentId === '3-arg1') ? 'argument-selected' : 'argument-unselected' ]" id="3-arg1" @click="fieldSelect('3-arg1')">
        {{ input[3].arg1 }}
      </div>
      <div v-bind:class="[ (this.currentId === '3-arg2') ? 'argument-selected' : 'argument-unselected' ]" id="3-arg2" @click="fieldSelect('3-arg2')">
        {{ input[3].arg2 }}
      </div>
    </div>
    <div class="row" id="row4">
      <div v-bind:class="[this.currentId==='4-function'?'function-selected':'function-unselected']" id="4-function" @click="fieldSelect('4-function')">
        {{ input[4].functionString }}
      </div>
      <div v-bind:class="[this.currentId === '4-arg1' ? 'argument-selected' : 'argument-unselected' ]" id="4-arg1" @click="fieldSelect('4-arg1')">
        {{ input[4].arg1 }}
      </div>
      <div v-bind:class="[ this.currentId === '4-arg2' ? 'argument-selected' : 'argument-unselected' ]" id="4-arg2" @click="fieldSelect('4-arg2')">
        {{ input[4].arg2 }}
      </div>
    </div>
    <div class="row" id="row5">
      <div v-bind:class="this.$props.fieldStates[5].function" id="5-function" @click="fieldSelect('5-function')">
        {{ input[5].functionString }}
      </div>
      <div v-bind:class="[this.currentId==='5-arg1'?'argument-selected':'argument-unselected']" id="5-arg1" @click="fieldSelect('5-arg1')">
        {{ input[5].arg1 }}
      </div>
      <div v-bind:class="[this.currentId==='5-arg2'?'argument-selected':'argument-unselected']" id="5-arg2" @click="fieldSelect('5-arg2')">
        {{ input[5].arg2 }}
      </div>
    </div>
    <button @click="submitGuess()">Submit Guess</button>
  </div>
</template>

<script>
export default {
  name: "GameRow",
  // Put data here
  props: {
    correct: Object,
    input: Object,
    isCurrentRow: Boolean,
    rowId: Number,
    fieldStates: Object,
  },
  methods: {
    // Sets current ID = 
    fieldSelect(field) {
      this.currentId = field;
      // Emit the row and whether it is a func or 1 of 2 arge
      this.$emit('fieldSelected', this.currentId);
    },
    submitGuess() {
      this.$emit('guessSubmitted');
    },
  }, 
  data: function() {
    return {
      currentId: "No field selected",
      fieldIDs: [
        "1-function", "1-arg1", "1-arg2",
        "2-function", "2-arg1", "2-arg2",
        "3-function", "3-arg1", "3-arg2",
        "4-function", "4-arg1", "4-arg2",
        "5-function", "5-arg1", "5-arg2",
      ],
      functionIDs: [
        "1-function",
        "2-function",
        "3-function",
        "4-function",
        "5-function",
      ],
      argumentIDs: [
        "1-arg1", "1-arg2",
        "2-arg1", "2-arg2",
        "3-arg1", "3-arg2",
        "4-arg1", "4-arg2",
        "5-arg1", "5-arg2",
      ]
    }
  }
};
</script>

<style scoped>
p {
  padding: 0px;
  margin: 0px;
}

.row {
  box-sizing: border-box;
  text-align: center;
  vertical-align: center;
}

.function-unselected {
  display: inline-block;
  width: 300px;
  height: 100px;
  background-color: #2b2b2b;
  color: #fff;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}

.function-selected {
  display: inline-block;
  width: 300px;
  height: 100px;
  background-color: #fff;
  color: #2b2b2b;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}

.argument-unselected {
  display: inline-block;
  width: 100px;
  height: 100px;
  background-color: #2b2b2b;
  color: #fff;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}

.argument-selected{
  display: inline-block;
  width: 100px;
  height: 100px;
  background-color: #fff;
  color: #2b2b2b;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}
</style>