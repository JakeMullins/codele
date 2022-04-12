<template>
  <div class="docs">
    <div id="toggle" @click="toggle()">
    </div>
    <div id="info" v-if="this.$props.toggled === true">
        <h1>
            Welcome to <code>Codele</code>
        </h1>
        <p>
            <code>Codele</code> is a game where you try to mimic an output given a set of initial conditions.
        </p>
        <p>
            Programming is the discipline of knowing the start conditions and the end conditions, and figuring out the steps in between in such a way that a computer can execute them. <code>Codele</code> brings the satisfaction of developing a bug free program without the soul-draining effort of actually learning how to <code>code</code>.
        </p>
        <p>
          In <code>Codele</code>, you will master the hottest new <code>language</code>, <code>C♭</code>. <code>C♭</code> is an esoteric <code>language</code> written by some guy named Lee. You will write a <code>C♭ program</code> in order to match the output given below. 
        </p>
        <p>
            Columns 1 is for <code>function</code> syntax. Columns 2 and 3 are for <code>arguments</code>.
        </p>
        <ul id="documentation">
            <li>
                <code>set</code>: <code>arg1</code> is assigned to <code>arg2</code>
            </li>
            <li>
                <code>add</code>: <code>arg2</code> is added to <code>arg1</code>
            </li>
            <li>
                <code>multiply</code>: <code>arg1</code> is multiplied by <code>arg2</code>
            </li>
            <li>
                <code>subtract</code>: <code>arg2</code> is subtracted from <code>arg1</code>
            </li>            <li>
                <code>print</code>: <code>arg1</code> is printed <code>arg2</code> times
            </li>

        </ul>

        <p>
            Upon hitting submit, the <code>interpreter</code> will run, executing your <code>code</code> and telling you some information about your entry.
        </p>
        <p>
            - A red box means that the <code>input</code> is invalid. Make sure that any function names are spelled correctly.
        </p>
        <div class="function-invalid-syntax">prnt</div>
        <p>
            - A green box means that the <code>input</code> is in the correct spot and valid.
        </p>
        <div class="function-correct">set</div>
        <p>
            - A yellow box means that the <code>input</code> is not in the correct spot, but is in the column somewhere else.
        </p>
        <div class="argument-different-spot">x</div>
        <p>
            - A gray box means that the <code>input</code> is valid, but not anywhere in the column
        </p>
        <div class="argument-unselected">4</div>
        <p>
            Some things to remember:
            <ol>
                <li>As designed, some solutions will match the desired <code>output</code>, but still not be correct. This means you'll have to come up with multiple ways to solve a problem.</li>
                <li>Yellow boxes only check if an <code>entry</code> is in the same column, not if it's in any other columns</li>
                <li>Blood for the Blood God</li>
            </ol>
        </p>
    </div>
  </div>
</template>

<style scoped>
    code {
        color: lime;
        background: bl;
        }
    p {
        text-align: left;
        font-size: 25px;
    }
    li {
        text-align: left;
        font-size: 25px;
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

.function-correct {
  display: inline-block;
  width: 300px;
  height: 100px;
  background-color: #538d4e;
  color: #2b2b2b;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}

.function-different-spot {
  display: inline-block;
  width: 300px;
  height: 100px;
  background-color: #b59f3b;
  color: #2b2b2b;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}

.function-invalid-syntax {
  display: inline-block;
  width: 300px;
  height: 100px;
  background-color: #f44646;
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

.argument-selected {
  display: inline-block;
  width: 100px;
  height: 100px;
  background-color: #fff;
  color: #2b2b2b;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}

.argument-correct {
  display: inline-block;
  width: 100px;
  height: 100px;
  background-color: #538d4e;
  color: #2b2b2b;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}

.argument-different-spot {
  display: inline-block;
  width: 100px;
  height: 100px;
  background-color: #b59f3b;
  color: #2b2b2b;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}

.argument-invalid-syntax {
  display: inline-block;
  width: 100px;
  height: 100px;
  background-color: #f44646;
  color: #2b2b2b;
  margin: 5px;
  font-size: 75px;
  vertical-align: middle;
}
</style>

<script>
export default {
  name: "DocsPanel",
  props: {
    toggled: Boolean
  },
  methods: {
    toggle() {
        this.$emit()
    }
  }
};
</script>