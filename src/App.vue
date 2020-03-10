<template>
  <div id="app">
    <Search />
    <div style="margin-top:68px">
      <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
    </div>
    <video-image />
    <camp-details />
  </div>
</template>

<script>
import Search from "./components/Search";
import VideoImage from "./components/VideoImage";
import CampDetails from "./components/CampDetails";

export default {
  name: "App",
  components: {
    Search,
    VideoImage,
    CampDetails
  }
};
</script>

<style>
body {
  margin: 0px;
  box-sizing: border-box;
}
* {
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
