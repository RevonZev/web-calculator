<template>
  <transition name="fade" appear>
    <div>
      <app-background></app-background>
      <app-calculator></app-calculator>
      <copyright></copyright>
    </div>
  </transition>
</template>

<script>
import AppBackground from "./components/AppBackground";
import AppCalculator from "./components/AppCalculator";
import Copyright from "./components/Copyright";

export default {
  name: "App",
  components: {
    "app-background": AppBackground,
    "app-calculator": AppCalculator,
    copyright: Copyright,
  },
};
</script>

<style>
body {
  font-family: "Roboto Condensed";
  margin: 0;
}
</style>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
