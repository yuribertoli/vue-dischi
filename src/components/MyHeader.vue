<template>
  <header>
      <img src="../assets/img/spotify-logo.png" alt="Spotify Logo">

        <!-- al cambio di un valore, la funzione change() invia il value dell'option (funzione specifica per questo tag, oltre ai tag input e textarea)  -->
        <!-- $event passa alla funzione di cui è argomento, l'oggetto relativo all'evento del DOM che si è verificato, in questo caso il cambio di value -->
      <select @change="valoreOption($event)">

          <!-- rendo la prima opzione non selezionabile, da usare come titolo soltanto -->
          <option class="titoletto" selected="false" disabled="disabled" value="scelta">Scegli un genere</option>

          <!-- ciclo i componenti dell'array per popolare dinamicamento le option-->
          <option 
                    v-for="(genere, indice) in generiAlbums" 
                    :key="indice" 
                    :value="genere">

                    {{genere}}
          </option>

      </select>
  </header>
</template>

<script>
export default {
    name: "MyHeader",
    props: { //ricevo da App l'array di generi inviato da Main
        'generiAlbums': Array
    },

    data(){
        return{
        }
    },

    methods: {

        //funzione per ottenere il value dell'opzione cliccata
        valoreOption(event){

            //invio ad App il valore del genere cambiato
            this.$emit('onClick', event.target.value);
        }
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