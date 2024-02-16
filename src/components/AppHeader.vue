
<script>
export default {
    name: 'AppHeader'
}
</script>

<template>
    <header>
        <nav class="d-flex">
            <div class="logo">
                <img src="https://vignette1.wikia.nocookie.net/yugiohenespanol/images/a/aa/Yugioh_anime_logo.jpg/revision/latest?cb=20130310042737&path-prefix=es"
                    alt="logo">
            </div>
            <h1>Yu-Gi-Oh API</h1>
        </nav>
    </header>
</template>


<style scoped>
header {
    filter: drop-shadow(0 0 10px black);
    position: fixed;
    width: 100%;
    top: 0;
    z-index: 10;
}

nav {
    background-color: var(--yugioh-white);
    align-items: center;
}

.logo {
    width: 80px;
    padding: 1rem;

    & img {
        width: 100%;
    }
}
</style>
