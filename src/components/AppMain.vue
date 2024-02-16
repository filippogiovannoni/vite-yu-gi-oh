<script>

import axios from 'axios'
import LoaderIcon from './LoaderIcon.vue'
import FilterOptions from './FilterOptions.vue'
import CardsFound from './CardsFound.vue'
import { store } from '../store.js'

export default {
    name: 'AppMain',
    data() {
        return {
            cardImage: [],
            cardImageUrl: [],
            base_api_url: 'https://db.ygoprodeck.com/api/v7/cardinfo.php?num=30&offset=0',
            store
        };
    },
    mounted() {
        this.getCards();
    },
    methods: {
        getCards() {
            axios
                .get(this.base_api_url)
                .then((response => {
                    console.log(response);
                    console.log(response.data);
                    console.log(response.data.data); // Card Info
                    store.cards = response.data.data;
                    store.cards.forEach(card => {
                        this.cardImage.push(card.card_images);
                    });
                    this.cardImage.forEach(cardUrl => {
                        this.cardImageUrl.push(cardUrl[0].image_url);
                    });
                    store.loading = false;
                }));
        }
    },
    components: { LoaderIcon, FilterOptions, CardsFound }
}
</script>

<template>
    <main>

        <div class="container">
            <FilterOptions v-if="!store.loading"></FilterOptions>
            <CardsFound v-if="!store.loading"></CardsFound>
            <LoaderIcon v-else></LoaderIcon>

            <div class="cards">
                <div class="row">
                    <div class="col-12 col-sm-6 col-md-4 col-lg-3" v-for="(card, index) in store.cards">
                        <div class="card">
                            <img :src="cardImageUrl[index]" alt="">
                            <div class="name">{{ card.name }}</div>
                            <div class="type">{{ card.archetype }}</div>
                        </div>
                    </div>
                </div>
            </div>

        </div>
    </main>
</template>


<style scoped>
main {
    position: relative;
    z-index: 0;
    padding-top: 3rem;
}

.name {
    color: var(--yugioh-white);
    text-align: center;
    text-transform: uppercase;
    font-weight: bold;
    margin: 0.5rem;
}

.type {
    text-align: center
}

.card:hover {
    scale: 1.05;
    transition: all 1s;
}
</style>