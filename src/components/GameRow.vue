<template>
  <div class="guess">
    <div class="row" v-for="row in rows" :key="row">
      <div class="function">
        <div class="function-tile"></div>
      </div>
      <div class="argument">
        <div class="argument-tile"></div>
      </div>
      <div class="argument">
        <div class="argument-tile"></div>
      </div>
    </div>
    <hr />
  </div>
</template>

<script>
export default {
  name: "GameRow",
  el: "#guess",
  data: () => {
    return {
      rows: [1, 2, 3, 4, 5],
    };
  },
  props: {
    yellow: String,
    green: Array,
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
}

.argument {
  display: inline-block;
  width: 100px;
  height: 100px;
  background-color: #2b2b2b;
  margin: 5px;
}
</style>