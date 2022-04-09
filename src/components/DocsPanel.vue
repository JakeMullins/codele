//

<template>
  <div class="docs">
    <div id="toggle" @click="toggle()">
        Help
    </div>
    <div id="info" v-if="this.$props.toggled === true">
        <h1>
            Welcome to <code>Codele</code>
        </h1>
        <p>
            <code>Codele</code> is a game where you try to mimic an output given a set of initial conditions.
        </p>
        <p>
            Programming is the discipline of knowing the start and the end, the pre and post conditions, and figuring out the steps in between in such a way that a computer can execute them. <code>Codele</code> brings the satisfaction of developing a bug free program without the soul-draining effort of actually learning how to <code>code</code>.
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
            </li>
            <li>
                <code>divide</code>: <code>arg1</code> is divided by <code>arg2</code>
            </li>
            <li>
                <code>print</code>: <code>arg1</code> is printed <code>arg2</code> times
            </li>

        </ul>

        <p>
            Upon hitting submit, the <code>interpreter</code> will run, executing your <code>code</code> and telling you some information about your entry.
        </p>
        <p>
            - A red box means that the <code>input</code> is invalid. Make sure that any function names are spelled correctly.
        </p>

        <p>
            - A green box means that the <code>input</code> is in the correct spot and valid.
        </p>
        <p>
            - A yellow box means that the <code>input</code> is not in the correct spot, but is in the column somewhere else.
        </p>
        <p>
            - A gray box means that the <code>input</code> is valid, but not anywhere in the column
        </p>
        <p>
            Some things to remember:
            <ol>
                <li>As designed, some solutions will match the desired <code>output</code>, but still not be correct</li>
                <li>Yellow boxes check if an <code>argument</code> is in the same column.</li>
                <li>Blood for the Blood God</li>
            </ol>
        </p>
    </div>
  </div>
</template>

<style scoped>
    code {
        color: lime;
    }
    p {
        text-align: left;
        font-size: 25px;
    }
    li {
        text-align: left;
    }
</style>

<script>
export default {
  name: "DocsPanel",
  props: {
    toggled: Boolean
  },
  method: {
    toggle() {
        this.$emit()
    }
  }
};
</script>