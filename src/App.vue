<template>
  <div id="app">
    <Header />
    <ChatArea />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import ChatArea from "./components/ChatArea.vue";

export default {
  name: "App",
  components: {
    Header,
    ChatArea
  }
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;600&display=swap");
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: "Montserrat", sans-serif;
}
</style>
