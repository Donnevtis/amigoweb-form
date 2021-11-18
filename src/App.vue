<script setup lang="ts">
import SingupForm from "./components/SingupForm.vue";
</script>

<template>
  <SingupForm />
</template>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:ital@0;1&family=IBM+Plex+Sans+Condensed:ital@0;1&family=IBM+Plex+Sans:ital,wght@0,100;0,400;0,700;1,100;1,400;1,700&family=IBM+Plex+Serif:ital@0;1&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: IBM Plex Sans, Avenir, Helvetica, Arial, sans-serif;
}
*::before,
*::after {
  box-sizing: border-box;
}
body {
  margin: 0;
  background-color: #2c3e50;
}

input:focus-visible {
  outline-offset: 0px;
}
input,
select,
a {
  border: none;
  text-decoration: none;
  background-color: transparent;
}
:focus-visible {
  outline-width: 0;
}
button {
  position: relative;
  border: none;
  padding: 0;
  cursor: pointer;
  &:focus {
    outline: none;
  }
}
ul {
  list-style-type: none;
}

#app {
  font-family: IBM Plex Sans, Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  // display: flex;
  // justify-content: center;
}
</style>
