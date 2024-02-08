<script>

import axios from 'axios'
import AppHeader from './components/AppHeader.vue'

export default {
  name: 'App',
  data() {
    return {
      cards: []
    }
  },
  mounted() {
    axios.
      get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0')
      .then((response => {
        console.log(response);
        console.log(response.data);
        console.log(response.data.data); // Card Info

        this.cards = response.data.data

        console.log(this.cards);

      }))
  },
  components: {
    AppHeader
  }
}
</script>

<template>
  <AppHeader></AppHeader>
  <main></main>
  <footer></footer>
</template>


<style></style>
