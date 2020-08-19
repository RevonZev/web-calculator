<template>
  <div class="copyright" v-on:click="changeName()">
    © 2020 {{ name }}
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "Revon Zev",
    }
  },
  methods: {
    changeName() {
      if (this.name == "Revon Zev") {
        this.name = "Senoaji Sapta Ramadhana";
      } else {
        this.name = "Revon Zev"
      }
    }
  },
};
</script>

<style scoped>
.copyright {
  position: absolute;
  bottom: 10px;
  left: 10px;
  color: white;
}
</style>
