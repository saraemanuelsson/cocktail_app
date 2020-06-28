<template lang="html">
    <div>
        <ul>
            <cocktail-list-item v-for="(cocktail, index) in displayCocktails" :cocktail="cocktail" :key="index"></cocktail-list-item>
        </ul>
    </div>
</template>

<script>
import CocktailListItem from "./CocktailListItem.vue";

export default {
    name: "cocktail-list",
    props: ["displayCocktails"],
    components: {
        "cocktail-list-item": CocktailListItem
    }

}
</script>

<style>

ul {
    margin: 0%;
    padding: 0%;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}

</style>