<template>
  <header class="header">
    <img src="../assets/logo.png" alt />
    <div>
      <input type="text" id="search" placeholder="Search" />
    </div>
    <div class="spacer"></div>
    <div>
      <a href>Get App</a>
    </div>
    <div>
      <a href>Near Me</a>
    </div>
    <div>
      <a href>Destination</a>
    </div>
    <div>
      <a href>Log In</a>
    </div>
  </header>
</template>
<style scoped>
img {
  width: 4.5vw;
}
#search {
  padding: 8px 10px;
  border-radius: 10px;
  width: 25vw;
  outline: none;
}
.header {
  display: flex;
  position: fixed;
  background: #fff;
  padding: 15px 30px 15px 30px;
  box-shadow: 0 3px 3px -3px black;
  top: 0;
  left: 0;
  right: 0;
}
.header > * {
  padding-left: 25px;
}
.header a {
  text-decoration: none;
  display: block;
  margin-top: 6px;
  padding-left: 10px;
}
.header a:hover {
  color: orange;
}
.spacer {
  flex: 1;
}
</style>