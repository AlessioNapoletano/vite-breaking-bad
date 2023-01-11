<script>
import { store } from '../store.js';
export default {
    name: 'CardComponent',

    props: {
        card: {
            type: Object,
            required: true
        }

    },

    data() {
        return {
            store,
        }
    }
}
</script>

<template>
    <div class="col-2">
        <div class="card" style="width: 18rem;">
            <img :src="card.card_images[0].image_url" :alt="card.name">
            <div class="card-body">
                <h5 class="card-title text-center">{{ card.name.toUpperCase() }}</h5>
                <p class="card-text text-center">{{ card.archetype }}</p>
            </div>
        </div>

    </div>


</template>

<style lang="scss" scoped>
.card-body {
    height: 100px;
    overflow: scroll;
}
</style>