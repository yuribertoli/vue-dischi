<template>
  <main>

    <!-- se la variabile caricamento è true, allora mostro l'immagine -->
    <div class="loading" v-if="caricamento">

        <div class="container">

            <img src="../assets/img/loading.png" alt="Loading">

        </div>
        
    </div>

    <div class="container" v-else>

        <div class="albums">

            <!-- ciclo l'array per ricavarne ogni oggetto presente, passo poi questi valori al componente figlio MyCard tramite la props :disco -->
            <MyCard :disco="album" v-for="(album, indice) in albums" :key="indice"/>

        </div>
        
    </div>

  </main>
</template>

<script>
import MyCard from "./partials/MyCard.vue";

const axios = require('axios').default;

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

            //effettuo una chiamata all'url indicato dalla variabile endpoint
            axios.get(this.endpoint)
                .then((risposta) => {
                    console.log(risposta);

                    //inserisco i dati dell'array nella variabile vuota albums
                    this.albums = risposta.data.response;

                    //imposto caricamento su false per far funzionare il v-if nell'html e non mostrare più il div di caricamento
                    this.caricamento = false;
                    console.log(this.albums);
            })
        }
    },

    //utilizzo computed per filtrare dei dati già posseduti in modo da ottimizzare le risorse e non dover effettuare la chiamata al server se i dati di partenza non sono cambiati
    computed: {

        //creo un array che prende come elementi i generi dell'array albums
        generi(){
            let generiMusicali = [];
            for (let i=0; i<this.albums.length; i++) {
                generiMusicali.push(this.albums[i].genre);
            }
            console.log('i generi musicali sono: ' + generiMusicali);
            return generiMusicali;
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