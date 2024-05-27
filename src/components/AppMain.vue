<script>
import SingleCard from '../components/AppMainComponents/SingleCard.vue'
import store from '../data/store.js';

export default {
    components: {
        SingleCard
    },
    data() {
        return {
            store
        }
    },
    methods: {

    },
    mounted() {
        // modifico il link creando 35 card e poi con un v-if al componente single card genero solo quelle dal 15 al 35
        axios.get("https://db.ygoprodeck.com/api/v7/cardinfo.php?num=35&offset=0").then(risultato => {
            risultato.data.data.forEach(element => {
                this.store.carte.push(element)
            });
            console.log(this.store.carte)
        });
    },
}
</script>

<template>
    <main>
        <div class="container-fluid">
            <div class="row">
                <div class="col-1"></div>
                <div class="col-1 py-4">
                    <select class="form-select" aria-label="Default select example">
                        <option selected>Tipo</option>
                        <option value="1">One</option>
                        <option value="2">Two</option>
                        <option value="3">Three</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="col-1"></div>
                <div class="col-10 p-5 bg-white">
                    <div class="bg-dark text-white p-3">Found 39 cards</div>

                    <div class="row m-0 gap-3">
                        <div v-for="element, index in store.carte" class="card border-0 p-0">
                            <SingleCard v-if="index >= 15 && index <= 35" :card="element" />
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