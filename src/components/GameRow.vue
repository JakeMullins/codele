<template>
  <div class="guess">
    {{ currSelected }}
    <div class="row" v-for="row in rows" :key="row">
      <div class="function">
        {{ functionString }}
      </div>
      <div class="argument">
        {{ arg1 }}
      </div>
      <div class="argument">
        {{ arg2 }}
      </div>
    </div>
    <hr />
  </div>
</template>

<script>
export default {
  name: "GameRow",
  data: () => {
    return {
      rows: [1, 2, 3, 4, 5],
    };
  },
  props: {
    correct: Object,
    row1: String,
    row2: String,
    row3: String,
    row4: String,
    row5: String,
    currSelected: Number,
  },
};
</script>

<style scoped>
p {
  padding: 0px;
  margin: 0px;
}

.row {
  grid-template-rows: repeat(6, 1fr);
  box-sizing: border-box;
  text-align: center;
}

.function {
  display: inline-block;
  width: 300px;
  height: 100px;
  background-color: #2b2b2b;
  margin: 5px;
  font-size: 75px;
}

.argument {
  display: inline-block;
  width: 100px;
  height: 100px;
  background-color: #2b2b2b;
  margin: 5px;
  font-size: 75px;
}
</style>