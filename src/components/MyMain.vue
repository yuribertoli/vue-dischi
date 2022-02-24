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
            <!-- mostro tramite v-show solo gli elementi che hanno il genere musicale uguale a quello selezionato nell'Header -->
            <MyCard v-show="album.genre.includes(valoreOptionRicevuto)" 
                    :disco="album" 
                    v-for="(album, indice) in albums" 
                    :key="indice"
            />

        </div>
        
    </div>

  </main>
</template>

<script>
import MyCard from "./partials/MyCard.vue";

const axios = require('axios').default;

export default {

    name: "MyMain",

    props: {
        "valoreOptionRicevuto": String
    },

    components: {
        MyCard
    },

    data() {
        return {
            albums: [],
            generiMusicali: [],
            artistiMusicali: [],
            caricamento: true,
            endpoint: 'https://flynn.boolean.careers/exercises/api/array/music'
        }
    },

    methods: {  
        pippo() {

            //effettuo una chiamata all'url indicato dalla variabile endpoint
            axios.get(this.endpoint)
                .then((risposta) => {

                    //inserisco i dati dell'array nella variabile vuota albums
                    this.albums = risposta.data.response;

                    //richiamo la funzione per prendere i generi musicali e gli artisti dagli albums
                    this.generi();
                    this.artisti();

                    //invio ad App i generi degli album e gli artisti
                    this.$emit('eventoGeneriAlbums', this.generiMusicali);
                    this.$emit('eventoArtistiAlbums', this.artistiMusicali);

                    //imposto caricamento su false per far funzionare il v-if nell'html e non mostrare più il div di caricamento
                    this.caricamento = false;
            })
        },

        //creo una funzione per ottenere i generi degli elementi nell'array albums
        generi(){
            
            for (let i=0; i<this.albums.length; i++) {

                //se il genere ciclato non è già presente nell'array generiMusicali lo aggiungo con push
                if (!this.generiMusicali.includes(this.albums[i].genre)) {
                    this.generiMusicali.push(this.albums[i].genre);
                } 
            }
            console.log('i generi musicali sono: ' + this.generiMusicali);
        },

        //creo una funzione per ottenere i nomi degli artisti negli elementi dell'array albums
        artisti(){
            
            for (let i=0; i<this.albums.length; i++) {

                //se l'artista ciclato non è già presente nell'array artistiMusicali lo aggiungo con push
                if (!this.artistiMusicali.includes(this.albums[i].author)) {
                    this.artistiMusicali.push(this.albums[i].author);
                } 
            }
            console.log('gli artisti sono: ' + this.artistiMusicali);
        }
    },

    //utilizzo computed per filtrare dei dati già posseduti in modo da ottimizzare le risorse e non dover effettuare la chiamata al server se i dati di partenza non sono cambiati
    computed: {  
    },

    //avvio al montaggio la funzione pippo
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