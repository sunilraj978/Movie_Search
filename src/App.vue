<template>
  <header>
    <div id="header">
      <h1 style="color:white"><span id="col">Vue</span> Movies</h1>
    </div>
  </header>
  <router-view />
</template>

<style lang="scss">
* {
  margin: 0px;
  padding: 0px;
}
body {
  background-color: #73a5c6;
}
#header {
  display: flex;
  justify-content: center;
  background-color: #23395d;
  padding: 10px;
}
#col {
  color: #00ff00;
}
</style>
