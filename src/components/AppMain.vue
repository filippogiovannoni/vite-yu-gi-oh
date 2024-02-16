<script>

import axios from 'axios'
import LoaderIcon from './LoaderIcon.vue'
import FilterOptions from './FilterOptions.vue'

export default {
    name: 'AppMain',
    data() {
        return {
            cards: [],
            cardImage: [],
            cardImageUrl: [],
            loading: true,
            base_api_url: 'https://db.ygoprodeck.com/api/v7/cardinfo.php?num=30&offset=0'
        };
    },
    mounted() {
        this.getCards();
    },
    computed: {
        cardsFound() {
            return this.cards.length > 0 ? 'Found ' + this.cards.length + ' cards' : 'No cards found';
        }
    },
    methods: {
        getCards() {
            axios
                .get(this.base_api_url)
                .then((response => {
                    console.log(response);
                    console.log(response.data);
                    console.log(response.data.data); // Card Info
                    this.cards = response.data.data;
                    this.cards.forEach(card => {
                        this.cardImage.push(card.card_images);
                    });
                    this.cardImage.forEach(cardUrl => {
                        this.cardImageUrl.push(cardUrl[0].image_url);
                    });
                    this.loading = false;
                    console.log(this.cardsFound);
                }));
        }
    },
    components: { LoaderIcon, FilterOptions }
}
</script>

<template>
    <main>

        <div class="container">
            <FilterOptions v-if="!loading"></FilterOptions>
            <div class="found" v-if="!loading">{{ cardsFound }}</div>
            <LoaderIcon v-else></LoaderIcon>

            <div class="cards">
                <div class="row">
                    <div class="col-12 col-sm-6 col-md-4 col-lg-3" v-for="(card, index) in cards">
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

.found {
    background-color: black;
    padding: 1rem;
    margin-top: 0.5rem;
    color: var(--yugioh-white);
    text-transform: uppercase;
    font-weight: bold;
}

.card:hover {
    scale: 1.05;
    transition: all 1s;
}
</style>