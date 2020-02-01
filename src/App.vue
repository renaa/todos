<template>
  <div id="app" :class="{runningTimer: runningInstances > 0}">
    <input
      id="createTimerName"
      class="createTimerName"
      type="text"
      v-on:keyup.enter="onClick()"
      v-model="inputTimerName"
    />

    <!-- <button @click="onClick">Click to insert</button> -->
    <div v-if="timerList.length > 0" class="container">
      <timer
        v-for="(time, index) in timerList"
        :key="time+index.toString()"
        v-on:onStart="onStart"
        v-on:onStop="onStop"
        v-on:destroyMe="removeTimer(index)"
        
        :timerName="time"
        :p='getRandomColor(75, 75)' 
        :s='getRandomColor(180, 75)'
      ></timer>
    </div>
  </div>
</template>

<script>
// import Vue from "vue";
import timer from "./components/timer.vue";

export default {
  name: "app",
  components: {
    timer
  },
  data: function() {
    return {
      inputTimerName: "",
      timerList: [],
      runningInstances: 0
    };
  },
  methods: {
    onClick: function() {
      this.timerList.push(this.inputTimerName);
      this.inputTimerName = "";
    },
    removeTimer: function(index) {
      this.timerList.splice(index, 1);
    },
    onStart: function() {
      this.runningInstances++;
    },
    onStop: function() {
      this.runningInstances--;
    },
    getRandomColor: function(value, variance) { // dont feed me numbers above 255 - variance/2

      var r = this.getrandomColorChannel(value, variance, false)
      var g = this.getrandomColorChannel(value, variance, false)
      var b = this.getrandomColorChannel(value, variance, false)
      var returnValue =  '#' + this.getHex(r) + this.getHex(g) + this.getHex(b)
      //console.log(returnValue, this.timerList.length)
      return returnValue
    },
    getrandomColorChannel(value, variance, toneDown){
      var x = Math.random()*variance*2 + value - variance;
      if (toneDown){
        x = x * 0.8;
      }
      return Math.floor(x)
    },
    getHex: function(value) {
      var hex = '00'
      if (value > 0 && value < 255){
        hex = value.toString(16) 
        if (hex.length < 2){
          hex = '0' + hex
        }
      }
      return hex
    }
    
  },
  created() {
    //var app = document.querySelector("#app");
    //app.style.setProperty("background", "#44af44");

  }
};
</script>

<style>
#app {
  --background-color: #af4444;
  --foreground-color: #000;
  position: fixed;
  padding: 50px 0 0 0;
  margin: 0;

  top: 0;
  left: 0;

  width: 100%;
  height: 100%;
  background: var(--background-color);

  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.runningTimer {
  background-color: #000;
}
.container {
  display: flex;
  flex-wrap: wrap;
  -ms-flex-align: center;
  flex-direction: row;
  justify-content: center;
}
.createTimerName {
  margin: 0 auto;
  text-align: center;
  font-size: 20px;
  display: block;
  background-color: transparent;
  border: 2px solid var(--foreground-color);
  color: var(--foreground-color);
  border-radius: 5px;
  padding: 5px;
  outline: 0;
}
</style>
