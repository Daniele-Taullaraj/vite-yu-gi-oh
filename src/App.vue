<script>
import AppHeader from './components/AppHeader.vue'
import AppMain from './components/AppMain.vue'
import store from './data/store.js';
import axios from 'axios';

export default {
  components: {
    AppHeader,
    AppMain
  },
  data() {
    return {
      store
    }
  },
  methods: {
    getCharacters() {
      axios.get("https://db.ygoprodeck.com/api/v7/cardinfo.php?num=35&offset=0").then(risultato => {
        risultato.data.data.forEach(element => {
          this.store.carte.push(element)
        });
      });
    },

    getArcheType() {
      axios.get("https://db.ygoprodeck.com/api/v7/archetypes.php?").then(risultato => {
        risultato.data.forEach(element => {
          this.store.archeTypes.push(element.archetype_name)
        });
      });
    }

  },
  mounted() {
    this.getCharacters()
    this.getArcheType()
  },
}

</script>

<template>
  <AppHeader />
  <AppMain :store="store" />
</template>

<style scoped></style>
