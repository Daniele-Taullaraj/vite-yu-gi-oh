<script>
import SingleCard from '../components/AppMainComponents/SingleCard.vue'
import store from '../data/store.js';
import axios from 'axios';

export default {
    components: {
        SingleCard
    },
    data() {
        return {
            store,
            selected: "",
            listaSelezionata: []
        }
    },
    methods: {
        checkType() {
            this.store.carte = []
            axios.get("https://db.ygoprodeck.com/api/v7/cardinfo.php?archetype=" + this.selected).then(risultato => {
                risultato.data.data.forEach(element => {
                    this.store.carte.push(element)
                });
                console.log(this.store.carte)
            });
        },
    },
    mounted() {

    },
}
</script>

<template>
    <main>
        <div class="container-fluid">
            <div class="row">
                <div class="col-1"></div>
                <div class="col-2 py-4">
                    <select class="form-select" aria-label="Default select example" @change="checkType()">
                        <option value="" disabled selected>Tipo</option>
                        <option v-for="tipo in store.archeTypes" :value="tipo">{{ tipo }}</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="col-1"></div>
                <div class="col-10 p-5 bg-white">
                    <div class="bg-dark text-white p-3">Found 39 cards</div>

                    <div class="row m-0 column-gap-3">
                        <div v-for="element, index in store.carte" class="card border-0 p-0">
                            <SingleCard :card="element" />
                        </div>
                    </div>

                </div>
                <div class="col-1"></div>
            </div>
        </div>

    </main>
</template>

<style scoped>
main {
    background-color: #D48F38;
}

.card {
    width: calc((100% - 4rem) / 5);
}
</style>