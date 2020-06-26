<template lang="html">
    <div>
        <cocktail-list-item v-for="cocktail in cocktails"></cocktail-list-item>
    </div>
</template>

<script>
import CocktailListItem from "./CocktailListItem"

export default {
    name: "cocktail-list",
    props: ["cocktails"],
    components: {
        "cocktail-list-item": CocktailListItem
    }

}
</script>

<style>

</style>