<template>
  <div id="app">
    <span>Create new task //todo pass name </span>
    <button @click="onClick">Click to insert</button>

    <div ref="container" class="container">
      <timer name="task1" />
      <timer name="task2" />
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import timer from "./components/timer.vue";

export default {
  name: "app",
  components: {
    timer
  },
  methods: {
    onClick() {
      var componentClass = Vue.extend(timer);
      var instance = new componentClass({
        propsData: { type: "primary" }
      });
      instance.$slots.default = ["click me!"];
      instance.$mount();
      this.$refs.container.appendChild(instance.$el);
    }
  }
};
</script>

<style>
#app {
  position: fixed;
  padding: 50px 0 0 0;
  margin: 0;

  top: 0;
  left: 0;

  width: 100%;
  height: 100%;
  background: blanchedalmond;

  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.container {
  display: flex;
  -ms-flex-align: center;
  flex-direction: row;
  justify-content: center;
}
</style>
