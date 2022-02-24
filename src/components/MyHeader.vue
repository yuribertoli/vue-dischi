<template>
  <header>
      <img src="../assets/img/spotify-logo.png" alt="Spotify Logo">

      <select>
          <option selected="false" disabled="disabled" value="scelta">Scegli un genere</option>
          <option v-for="(genere, indice) in generiAlbums" :key="indice" :value="genere">
              {{genere}}
          </option>
      </select>
  </header>
</template>

<script>
export default {
    name: "MyHeader",
    props: {
        'generiAlbums': Array
    }
}
</script>

<style scoped lang="scss">
@import "../assets/style/variables.scss";

    header {
        display: flex;
        justify-content: space-between;
        height: 50px;
        background-color: $color1;

        img {
            height: 80%;
            width: auto;
            padding: 10px 0 0 20px;
        }

        select {
            height: 30px;
            margin: 10px 30px 0 0;
            width: 150px;
            color: black;

            option {
                color: black;
            }
        }
    }
</style>