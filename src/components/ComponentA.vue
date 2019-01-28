<template>
  <div class="hello">
    <h1>{{msg}}</h1>
    <h1 v-text="ruiBaby"></h1>
    <button v-on:click="onClickMe">Click Mouse!</button>
  </div>
</template>

<script>
export default {
  name: 'ComponentA',
  data () {
    return {
      msg: 'Hello from component a!',
      words: 'She will love me forever!'
    }
  },
  // 父向子组件传参
  props: ['ruiBaby'],
  methods: {
    onClickMe: function () {
      //console.log(this.ruiBaby)
      // 子向父组件传参($emit(): 在它上面触发事件)
      this.$emit('lover-tell-me-something', this.words);
      // $dispatch(): 派发事件，事件沿父链冒泡,(1.x版本可用)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
