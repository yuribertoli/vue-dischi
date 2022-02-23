<template>
  <div class="card">

      <img :src="disco.poster" :alt="disco.author + ' - ' + disco.title">

      <h3>{{disco.title}}</h3>

      <span>{{disco.author}}</span>

      <span>{{disco.year}}</span>

  </div>
</template>

<script>
export default {

    name: "MyCard",

    props: {
        "disco": Object
    }
}
</script>

<style scoped lang="scss">
@import "../../assets/style/variables.scss";

.card {
    width: calc(20% - 50px);
    height: 300px;
    padding: 10px;
    margin: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: $color1;

    img {
        width: 100%;
        height: auto;
    }
    h3 {
        margin: 10px 0;
        text-transform: uppercase;
        text-align: center;
    }
    span {
        color: grey;
        font-size: 0.8rem;
    }
}

</style>