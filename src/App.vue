<template>
  <div>
    <app-background></app-background>
    <app-calculator></app-calculator>
  </div>
</template>

<script>
import AppBackground from "./components/AppBackground";
import AppCalculator from "./components/AppCalculator";

export default {
  name: "App",
  components: {
    "app-background": AppBackground,
    "app-calculator": AppCalculator,
  },
};
</script>

<style>
body {
  margin: 0;
}
</style>
