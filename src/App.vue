<template>
  <div id="app">
    <form v-on:submit.prevent="onSubmit">
      <input size="80" v-model="privateKey" placeholder="edit me">
      <button type='submit'>Submit</button>
      <br/>
      <span>{{mnemonic}}</span>
    </form>
  </div>
</template>

<script>
import * as Mnemonic from 'bitcore-mnemonic';
import {HDPrivateKey} from 'bitcore-lib';
export default {
  name: 'app',
  data () {
    return {
      privateKey: '', 
      mnemonic: ''
    }
  },
  methods: {
    onSubmit: function(event) {
      var mnemonic = Mnemonic.fromSeed(new HDPrivateKey(this.privateKey).privateKey.toBuffer(), Mnemonic.Words.CHINESE);
      this.mnemonic = mnemonic.toString();
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

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
