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

    <div v-for="card in store.cardList">
        <p>
            {{ card.card_images.image_url }}
        </p>


    </div>

</template>

<style lang="scss" scoped>

</style>