<template>
  <div id="app">
    <input id='createTimerName' class='createTimerName' type='text' v-on:keyup.enter="onClick(event)" v-model="inputTimerName" /> 

    <!-- <button @click="onClick">Click to insert</button> -->
    <div v-if="timerList.length > 0"  ref="container" class="container">

    <timer :timerName='time' v-for="(time,i) in timerList" :key="i">
        <input type="text">
    </timer>
      
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
        inputTimerName: '',
        timerList: []
      }
  },
  methods: {
    onClick: function() {
    this.timerList.push(this.inputTimerName);
    this.inputTimerName = ''
    },
    doLOLS: function(){
      console.log("CLICK FROM OUTSIDE OF COMPONENT");
    }
  },
  created(){

    var app = document.querySelector("#app");
    app.style.setProperty('background', "#44af44");
    console.log("....")
    console.log("background", "#aaa" )
  },
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
  border:2px solid var(--foreground-color);
  color: var(--foreground-color);
  border-radius: 5px;
  padding: 5px;
  outline: 0;
}
</style>
