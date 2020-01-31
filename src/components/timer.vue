<template>
  <div class="timer" :class='{activetimer: running}'>
    <!-- //https://github.com/vuejs/vue/issues/6677    error: v-bind without argument expects an Object or Array value: -->
    <input class='name' :class='{activetimer: running}' type='text' :value='dataTimerName'/> 
  <div>{{dataTimerName}}</div>
    <button class="timer-button" :class='{active: running}' @click="start">start</button>
    <button class="timer-button" :class='{active: !running}' @click="stop">stop</button>
    <div class="counter" :class='{activecounter: running}'>{{displayTime}}</div>

    <button class="destroy-button" v-on:click='destroy'>X</button> <!-- //todo implement destroy -->
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "timer",
  props: {
    timerName: String
  },
  data() {
    return {
      dataTimerName: '',
      running: false,
      startTime: 0,
      displayTime: '00:00:00',
      counter: 0,
      timerFunction: Function
    };
  },
  created: function() {
      this.dataTimerName = this.timerName
  },

  methods: {
    start: function(event) {
        console.log("hello from inside comp");

        this.$emit('onStart', event);
      if (!this.running) {
        this.running = true;
        this.timerFunction = setInterval(this.updateTime, 1000);
      }
    },

    updateTime: function() {
      ++this.counter;
      this.displayTime = this.prettyDisplay(this.counter);
    },
    prettyDisplay(c){
      var sec_num = parseInt(c, 10); // don't forget the second param
      var hours   = Math.floor(sec_num / 3600);
      var minutes = Math.floor((sec_num - (hours * 3600)) / 60);
      var seconds = sec_num - (hours * 3600) - (minutes * 60);

      if (hours   < 10) {hours   = "0"+hours;}
      if (minutes < 10) {minutes = "0"+minutes;}
      if (seconds < 10) {seconds = "0"+seconds;}
      return hours+':'+minutes+':'+seconds;
    },
    stop: function() {
      if (this.running) this.running = false;
      clearInterval(this.timerFunction);
    },
    destroy: function() {
      //todo
      this.$el.parentNode.removeChild(this.$root.$el)
    }
  },
  
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped >

.timer {
  /* primary and secondary color */
  --p:  #267552;
  --s: #a5e7bb;
  --p:  #740c54;
  --s: #ecd46b;
  --p:  #421e09;
  --s: #ebb38d;
  --p:  #3b3735;
  --s: #dbcabe;
  position: relative;
  padding: 20px 25px 20px 20px;
  margin: 10px;
  border: 2px solid var(--p);
  width: fit-content;
  border-radius: 5px;
  background-color: var(--s);
}
.name {
  text-align: center;
  font-size: 20px;
  display: block;
  background-color: var(--s);
  border:2px solid var(--p);
  color: var(--p);
  border-radius: 5px;
  margin:  10px;
  padding: 5px;
  outline: 0;
}

.counter {
  padding: 15px 0 0;
  font-size: 25px;
  color: var(--p);
}
.activecounter {
  font-weight: bold ;
}
.timer-button {
  border: none;
  background-color: var(--s);
  cursor: pointer;
  color: var(--p);
  font-size: 16px;
  padding: 10px;
  margin: 10px;
  border-radius: 3px;
  border: 2px solid var(--p);
}
.active{
  background-color: var(--p);
  color:var(--s);
}
.timer-button:focus {
  outline: 0;
  
}
.destroy-button {
  border: none;
  background-color: #0000;
  color: var(--p);
  position: absolute;
  top: -2px;
  right: -2px;
  border: 2px solid var(--p);
  border-radius: 5px;
  padding: 5px 8px;

}
.destroy-button:focus{
  outline: 0;
}
</style>
