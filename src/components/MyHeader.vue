<template>
  <header>
      <img src="../assets/img/spotify-logo.png" alt="Spotify Logo">
  </header>
</template>

<script>
export default {
    name: "MyHeader"
}
</script>

<style scoped lang="scss">
@import "../assets/style/variables.scss";

    header {
        height: 50px;
        background-color: $color1;

        img {
            height: 80%;
            width: auto;
            padding: 10px 0 0 20px;
        }
    }
</style>