<template>
  <div>
    <app-background></app-background>
    <app-calculator></app-calculator>
    <copyright></copyright>
  </div>
</template>

<script>
import AppBackground from "./components/AppBackground";
import AppCalculator from "./components/AppCalculator";
import Copyright from './components/Copyright'

export default {
  name: "App",
  components: {
    "app-background": AppBackground,
    "app-calculator": AppCalculator,
    "copyright": Copyright,
  },
};
</script>

<style>
body {
  font-family: "Roboto Condensed";
  margin: 0;
}
</style>
