<template>
  <div class="hello">
    <h1>{{ msg }} .</h1>
    <button v-on:click="start">start</button>
    <button v-on:click="stop">stop</button>
    <dir>{{counter}}</dir>
  </div>
</template>

<script>
export default {
  name: 'test',
  props: {
    msg: String,
    x: Number,
  },
  data() {
    return {
      running: false,
      counter: 0,
      startTime: 0,
    };
  },
  methods: {
    start: function() {
     this.startTime = Date.now()
     this.running = true
    }, 
    stop: function() {

      if(this.running){
        this.counter = Date.now() - this.startTime;
        this.running = false;
      }
      
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
