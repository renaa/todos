<template>
  <div class="timer" :class="{activetimer: running}" :style="pVal">
    <input class="name" :class="{activetimer: running}" type="text" v-model="dataTimerName" />
    <button class="timer-button" :class="{active: running}" @click="start">start</button>
    <button class="timer-button" :class="{active: !running}" @click="stop">stop</button>
    <div class="counter" :class="{activecounter: running}">{{displayTime}}</div>
    <button class="destroy-button" v-on:click="$emit('destroyMe')">X</button>
  </div>
</template>

<script>
export default {
  name: "timer",
  props: {
    timerName: String,
    p: String,
    s: String
  },
  data() {
    return {
      dataTimerName: "",
      running: false,
      startTime: 0,
      displayTime: "00:00:00",
      counter: 0,
      timerFunction: Function,
      dataP: '#000000',
      dataS: '#ffffff',
    };
  },
  created: function() {
    this.dataTimerName = this.timerName;
    this.dataP = this.p;
    this.dataS = this.s;
  },
  computed: {
    pVal() {
      return {
        '--p':this.dataP,
        '--s':this.dataS
      }
    },
  },
  methods: {
    start: function(event) {
      if (!this.running) {
        this.$emit("onStart", event);
        this.running = true;
        this.timerFunction = setInterval(this.updateTime, 1000);
      }
    },
    stop: function() {
      if (this.running) {
        this.$emit("onStop", event);
        this.running = false;
        clearInterval(this.timerFunction);
      }
    },
    updateTime: function() {
      ++this.counter;
      this.displayTime = this.prettyDisplay(this.counter);
    },
    prettyDisplay(c) {
      var sec_num = parseInt(c, 10); // don't forget the second param
      var hours = Math.floor(sec_num / 3600);
      var minutes = Math.floor((sec_num - hours * 3600) / 60);
      var seconds = sec_num - hours * 3600 - minutes * 60;

      if (hours < 10) hours = "0" + hours;
      
      if (minutes < 10) minutes = "0" + minutes;
      
      if (seconds < 10) seconds = "0" + seconds;
      
      return hours + ":" + minutes + ":" + seconds;
    },
  }
};
</script>
<style scoped >
.timer {
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
  border: 2px solid var(--p);
  color: var(--p);
  border-radius: 5px;
  margin: 10px;
  padding: 5px;
  outline: 0;
}
.counter {
  padding: 15px 0 0;
  font-size: 25px;
  color: var(--p);
}
.activecounter {
  font-weight: bold;
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
.active {
  background-color: var(--p);
  color: var(--s);
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
.destroy-button:focus {
  outline: 0;
}
</style>
