<template>
  <main>

    <div class="loading" v-if="caricamento">

        <div class="container">

            <img src="../assets/img/loading.png" alt="Loading">

        </div>
        
    </div>

    <div class="container" v-else>

        <div class="albums">

            <MyCard :disco="album" v-for="(album, indice) in albums" :key="indice"/>

        </div>
        
    </div>

  </main>
</template>

<script>
import MyCard from "./partials/MyCard.vue";

const axios = require('axios');

export default {

    name: "MyMain",

    components: {
        MyCard
    },

    data() {
        return {
            albums: [],
            caricamento: true,
            endpoint: 'https://flynn.boolean.careers/exercises/api/array/music'
        }
    },

    methods: {  
        pippo() {
            axios.get(this.endpoint)
                .then((risposta) => {
                    console.log(risposta);
                    this.albums = risposta.data.response;
                    this.caricamento = false;
                    console.log(this.albums);
            })
        }
    },

    mounted() {
        this.pippo();
    }
}
</script>

<style scoped lang="scss">
.loading {
    .container {
        display: flex;
        justify-content: center;

        img {
            padding-top: 10%;
        }
    }
}

.albums {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
}

</style>