<template lang="html">
    <div>
        <h2>Browse Cocktails</h2>
        <ul>
            <cocktail-list-item v-if="cocktails[index] != null" v-for="(cocktail, index) in cocktails" :cocktail="cocktail" :key="index"></cocktail-list-item>
        </ul>
    </div>
</template>

<script>
import CocktailListItem from "./CocktailListItem.vue";

export default {
    name: "cocktail-list",
    props: ["cocktails"],
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