<template>
  <router-view />
</template>

<script>
export default {
  methods: {},
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html,
body {
  height: 100vh;
}

#app {
  font-family: "Poppins", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #333;

  display: flex;
  justify-content: center;
  align-items: center;

  width: 100%;
  height: 100%;
}

body {
  background-color: #222;
}
</style>
