<script>

import axios from 'axios'

export default {
    name: 'AppMain',
    data() {
        return {
            cards: [],
            cardImage: [],
            cardImageUrl: [],
            loading: true
        }
    },
    mounted() {

        setTimeout(() => {
            axios
                .get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=30&offset=0')
                .then((response => {
                    console.log(response);
                    console.log(response.data);
                    console.log(response.data.data); // Card Info

                    this.cards = response.data.data

                    this.cards.forEach(card => {
                        this.cardImage.push(card.card_images)
                    })

                    this.cardImage.forEach(cardUrl => {
                        this.cardImageUrl.push(cardUrl[0].image_url)
                    })
                    this.loading = false

                    console.log(this.cardsFound);

                }))
        }, 1000)
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
            <div class="filters" v-if="!loading">
                <select name="type" id="type">
                    <option value="All" selected>All</option>
                    <option value="Alien">Alien</option>
                    <option value="Infernoble Arms">Infernoble Arms</option>
                    <option value="Noble Knight">Noble Knight</option>
                    <option value="Melodious">Melodious</option>
                    <option value="Archfiend">Archfiend</option>
                    <option value="Elemental HERO">Elemental HERO</option>
                    <option value="Umi">Umi</option>
                    <option value="ABC">ABC</option>
                </select>
                <input type="text" name="searchBox" id="searchBox" placeholder="Enter card name">
                <button>Search</button>
            </div>
            <div class="found" v-if="!loading">{{ cardsFound }}</div>
            <div class="loader" v-else>
                Loading Cards...
                <i class="fa-solid fa-spinner fa-spin"></i>
            </div>

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
.filters {
    margin: 2rem 0;
    display: flex;
    gap: 1rem;

    & select,
    input,
    button {
        padding: 0.5rem;
        border-radius: 0.5rem;
        border-style: none;
        filter: drop-shadow(0 0 5px black);
    }
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

.card:hover {
    scale: 1.05;
    transition: all 1s;
}
</style>