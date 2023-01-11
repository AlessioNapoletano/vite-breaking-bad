<script>
//sotto component necessario per creare una carta
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
        <div class="cards-number w-100 d-flex justify-content-center">
            <h1 class="text-center p-2">
                Numero di carte trovate: {{ store.cardList.length }}
            </h1>
        </div>

        <article class="d-flex flex-wrap justify-content-center">
            <CardComponent class="m-2" v-for="card in store.cardList" :card="card" />
        </article>

    </div>


</template>

<style lang="scss" scoped>
@use '../styles/partials/variables' as *;

.wrapper {
    background-color: $main-bg-color;

    h1 {
        border-radius: 20px;
        background-color: black;
        color: white;
    }

    .card-body {
        height: 100px;
    }
}
</style>