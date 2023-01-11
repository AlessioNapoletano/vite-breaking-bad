<script>
import CardComponent from './CardComponent.vue';
import { store } from '../store.js'
import axios from 'axios';


export default {
    name: 'AppMain',

    components: {
        CardComponent,
    },

    data() {
        return {
            store,
            url: 'https://db.ygoprodeck.com/api/v7/cardinfo.php?num=10&offset=0',

        }
    },

    methods: {
        getCard() {
            axios.get(this.url, {})
                .then((response) => {
                    console.log(response.data.data);
                    this.store.cardList = response.data.data;

                })
                .catch(function (error) {
                    console.log(error);
                })
        }

    },

    created() {
        this.getCard();
    }

}
</script>

<template>
    <div class="wrapper d-flex flex-wrap justify-content-center py-5">
        <article v-for="card in store.cardList" class="mx-4 my-3">
            <div class="card" style="width: 18rem;">
                <img :src="card.card_images[0].image_url" :alt="card.name">
                <div class="card-body">
                    <h5 class="card-title text-center">{{ card.name }}</h5>
                    <p class="card-text text-center">{{ card.archetype }}</p>
                </div>
            </div>
        </article>

    </div>


</template>

<style lang="scss" scoped>
.wrapper {
    background-color: #bf9248;

    .card-body {
        height: 100px;
    }
}
</style>