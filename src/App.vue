<template>
  <div id="app">
    <img src="./assets/logo.png">
    <HelloWorld/>
    <h1 v-html="title"></h1>
    <ul>
      <li  v-for="item in items" v-bind:class="{finished: item.isFinish}" v-on:click="toggleFinish(item)">
        {{item.label}}
      </li>
    </ul>
    <input v-model="newItem" v-on:keyup.enter="addNew"/>
    <ComponentA ruiBaby="I love Rui forever" v-on:lover-tell-me-something="listenToHer"> </ComponentA>
    <p>lover tells me : {{loverWords}}</p>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import Store from './store'
import ComponentA from './components/ComponentA'

console.log(Store)
export default {
  data: function () {
    return {
      title: '<span>?</span>this is a todo list',
      items: Store.fetch(),
      newItem: '',
      loverWords: ''
    }
  },
  methods: {
    toggleFinish: function (item) {
      item.isFinish = !item.isFinish
    },
    addNew: function () {
      this.items.push({
        label: this.newItem,
        isFinish: false
      })
      this.newItem = ''
    },
    listenToHer: function (msg) {
      this.loverWords = msg
    }
  },
  watch: {
    items: {
      handler: function (items) {
        Store.save(items)
      },
      deep: true
    }
  },
  name: 'App',
  components: {
    HelloWorld,
    ComponentA
  }
}
</script>

<style>
.finished{
    text-decoration: underline;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
