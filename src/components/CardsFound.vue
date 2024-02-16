<script>

import { store } from '../store.js'

export default {
    name: 'CardsFound',
    data() {
        return {
            store
        }
    },
    computed: {
        cardsFound() {
            return store.cards.length > 0 ? 'Found ' + store.cards.length + ' cards' : 'No cards found';
        }
    },
}
</script>
<template>
    <div class="found" v-if="!store.loading">{{ cardsFound }}</div>
</template>


<style scoped>
.found {
    background-color: black;
    padding: 1rem;
    margin-top: 0.5rem;
    color: var(--yugioh-white);
    text-transform: uppercase;
    font-weight: bold;
}
</style>