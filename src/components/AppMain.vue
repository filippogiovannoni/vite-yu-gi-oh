<script>

import axios from 'axios'

export default {
    name: 'AppMain',
    data() {
        return {
            cards: [],
            cardImage: [],
            cardImageUrl: [],
            selectOptions: new Set([])
        }
    },
    mounted() {
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

            }))

    }
}
</script>

<template>
    <main>

        <div class="container">
            <select name="type" id="type">
                <option v-for="option in selectOptions" value="">{{ option }}</option>
            </select>

            <div class="founded">Found {{ cards.length }} cards</div>

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

.founded {
    background-color: black;
    padding: 1rem;
    margin-top: 0.5rem;
    color: var(--yugioh-white);
    text-transform: uppercase;
    font-weight: bold;
}
</style>