<script>
export default {
    props: {
        card: Object
    },
    data() {
        return {
        }
    },
    methods: {

    },
    mounted() {
    }
}

</script>

<template>

    <img :src="card.card_images[0].image_url" alt="" class="w-100">
    <div class="card-bg text-white text-center p-3 h-100 d-flex flex-column justify-content-between">
        <h6>{{ card.name }}</h6>
        <span class="text-dark">{{ card.race }}</span>
    </div>

</template>

<style scoped>
.card-bg {
    background-color: #D48F38;
}
</style>