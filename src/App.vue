<template>
  <div id="app">
    <MyHeader :generiAlbums="arrayGeneri"/> <!-- mando all'header arrayGeneri tramite la props generiAlbums -->
    <MyMain @eventoGeneriAlbums="popolaArrayApp"/> <!-- all'evento richiamo la funzione popolaArrayApp -->
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
    return { //creo un array vuoto per popolarlo con i valori ricevuti da Main e da inviare poi a Header
      arrayGeneri: []
    }
  },

  methods: {

    //funzione per prendere i valori ricevuti da $emit in Main e popolare arrayGeneri
    popolaArrayApp(valore){
      this.arrayGeneri = valore;
      console.log("array in App: " + this.arrayGeneri);
    }
  }
}
</script>

<style lang="scss">
 @import "./assets/style/general.scss";
</style>
