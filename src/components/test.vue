<template>
  <div class="hello">
    <h1>{{ msg }} .</h1>
    <button v-on:click="start">start</button>
    <button v-on:click="stop">stop</button>
    <dir>
      <span>{{timer}}
      </span>
      </dir>
  </div>
</template>

<script>
export default {
  name: 'test',
  props: {
    msg: String,
    
  },
  data() {
    return {
      running: false,
      startTime: 0,
      displayTime: 0,
      timer: 0,
      timerFunction: Function
    };
  },
  computed: {
    
  },
  
  methods: {
    start: function() {
    this.running = true;
    this.timerFunction = setInterval(this.updateTime, 1000); 
    
    }, 

    updateTime: function() {
    ++this.timer;
    this.displayTime = this.timer;
    },

    stop: function() {
      if(this.running)
        this.running = false; 
        clearInterval(this.timerFunction)       
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
