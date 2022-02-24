<template>
  <div id="app">

    <!-- invio all'Header arrayGeneri tramite la props generiAlbums -->
    <!-- all'evento onClick di Header richiamo la funzione selezioneValueSelect -->
    <MyHeader :generiAlbums="arrayGeneri" @onClick="selezioneValueSelect"
              :artistiAlbums="arrayArtisti" @ArtistClick="selezioneArtistaSelect"/> 
    <!-- invio ad Header i nomi degli artisti tramite la props artistiAlbums -->
    <!-- ricevo il valore dell'artista selezionato e richiamo la funzione selezioneArtistaSelect -->


    <!-- all'evento richiamo la funzione popolaArrayApp -->
    <!-- invio al Main il valore dell'option selezionata tramite la props valoreOptionRicevuto -->
    <MyMain @eventoGeneriAlbums="popolaArrayApp" :valoreOptionRicevuto="valoreOpzione"
            @eventoArtistiAlbums="nomiArtisti" :valoreArtistaRicevuto="valoreArtista"/> 
    <!-- ricevo da eventoArtistiAlbums un array e richiamo la funzione nomiArtisti -->
    <!-- invio al Main il valore dell'artista selezionato tramite la props valoreArtistaRicevuto -->

  </div>
</template>

<script>
import MyHeader from './components/MyHeader.vue'
import MyMain from './components/MyMain.vue'

export default {
  name: 'App',
  components: {
    MyHeader,
    MyMain
  },

  data(){
    return { 
      
      //creo un array vuoto per popolarlo con i valori ricevuti da Main e da inviare poi a Header
      //faccio la stessa cosa per i nomi degli artisti
      arrayGeneri: [],
      arrayArtisti: [],

      //creo una variabile da popolare con il value dell'option cliccata nell'header
      //poi una per il nome dell'artista selezionato
      valoreOpzione: "",
      valoreArtista: ""
    }
  },

  methods: {

    //funzione per prendere i valori ricevuti da $emit in Main e popolare arrayGeneri
    popolaArrayApp(valore){
      this.arrayGeneri = valore;
      console.log("array in App: " + this.arrayGeneri);
    },

    //funzione per popolare la variabile valoreOpzione e inviarne il contenuto a Main
    selezioneValueSelect(valore){
      this.valoreOpzione = valore;
      console.log("valore nell'option: " + this.valoreOpzione);
    },



    //funzione per prendere i valori ricevuti da $emit in Main e popolare arrayArtisti
    nomiArtisti(valore){
      this.arrayArtisti = valore;
    },

    //inoltro alla variabile valoreArtista il valore dell'artista selezionato
    selezioneArtistaSelect(valore){
      this.valoreArtista = valore;
      console.log("valore nell'option artisti: " + this.valoreArtista);
    }
  }
}
</script>

<style lang="scss">
 @import "./assets/style/general.scss";
</style>
