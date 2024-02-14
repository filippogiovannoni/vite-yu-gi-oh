<script>

import axios from 'axios'

export default {
    name: 'AppMain',
    data() {
        return {
            cards: [],
            cardImage: [],
            cardImageUrl: [],
            selectOptions: new Set([]),
            loading: true
        }
    },
    mounted() {

        setTimeout(() => {
            axios
                .get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0')
                .then((response => {
                    console.log(response);
                    console.log(response.data);
                    console.log(response.data.data); // Card Info

                    this.cards = response.data.data

                    this.cards.forEach(card => {
                        this.cardImage.push(card.card_images)
                        this.selectOptions.add(card.archetype)
                    })

                    this.cardImage.forEach(cardUrl => {
                        this.cardImageUrl.push(cardUrl[0].image_url)
                    })
                    this.loading = false

                    console.log(this.cardsFound);

                }))
        }, 3000)
    },
    computed: {
        cardsFound() {
            return this.cards.length > 0 ? 'Found ' + this.cards.length + ' cards' : 'No cards found'
        }
    }
}
</script>

<template>
    <main>

        <div class="container">
            <select name="type" id="type" v-if="!loading">
                <option v-for="option in selectOptions" value="">{{ option }}</option>
            </select>
            <div class="found" v-if="!loading">{{ cardsFound }}</div>
            <div class="loader" v-else>
                Loading Cards...
                <i class="fa-solid fa-spinner fa-spin"></i>
            </div>

            <div class="cards">
                <div class="row">
                    <div class="col-2" v-for="(card, index) in cards">
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
select {
    margin: 2rem 0;
    padding: 0.5rem;
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

.loader {
    height: 90vh;
    display: flex;
    justify-content: center;
    align-items: center;

    & i {
        padding: 0 0.5rem;
    }
}
</style>