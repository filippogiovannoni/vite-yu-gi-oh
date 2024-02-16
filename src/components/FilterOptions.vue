<script>
export default {
    name: 'FilterOptions'
}
</script>

<template>
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
</style>