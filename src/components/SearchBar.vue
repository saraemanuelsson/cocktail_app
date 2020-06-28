<template lang="html">
  <div>
      <input type="text" v-model="searchTerm" placeholder="Search for">
      <button v-on:click="searchDrinkName(searchTerm)">Search by name</button>
      <button v-on:click="searchIngredient(searchTerm)">Search by ingredient</button>
      <button v-on:click="viewAll()">View All</button>
  </div>
</template>

<script>
import {eventBus} from "../main.js"

export default {
    name: "search-bar",
    props: ["cocktails"],
    data() {
        return {
            searchTerm: "",
            foundCocktails: []
        }
    },
    methods: {

        searchDrinkName(searchName) {
            this.foundCocktails = this.cocktails.filter(cocktail => cocktail.strDrink === searchName);
            eventBus.$emit("cocktails-found", this.foundCocktails);
            this.searchTerm = "";
        },

        searchIngredient(searchIngredient) {
            this.foundCocktails = this.cocktails.filter(cocktail => {
                if (this.cocktailIngredients(cocktail).includes(searchIngredient))
                return cocktail
            })
            eventBus.$emit("cocktails-found", this.foundCocktails);
            this.searchTerm = "";
        },

        cocktailIngredients(cocktail) {

            const cocktailKeys = Object.keys(cocktail);
            const ingredientKeys = cocktailKeys.filter(key => key.includes("Ingredient"));

            const ingredients = [];

            for (const key of ingredientKeys) {
                if (cocktail[key] != null) {
                    ingredients.push(cocktail[key])
                }
            }

            return ingredients;
        },

        viewAll() {
            eventBus.$emit("cocktails-found", this.cocktails)
        }
    }
}
</script>

<style>

</style>