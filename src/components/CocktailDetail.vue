<template>
  <div class="drink-recipe">
    <cocktail-name class="name" :cocktail="cocktail"></cocktail-name>
    <div id="button">
        <button v-on:click="displayForm">I Made This!</button>
    </div>
    <cocktail-pic class="pic" :cocktail="cocktail"></cocktail-pic>
    <div>
        <ul id="ingredients" v-for="(measure, index) in getIngredients('Measure')">
            <li>{{measure}}{{getIngredients('Ingredient')[index]}}</li>
        </ul>
    </div>
    <p id="method">{{cocktail.strInstructions}}</p>
  </div>
</template>

<script>
import CocktailPic from "./CocktailPic"
import CocktailName from "./CocktailName"

export default {
    name: "cocktail-detail",
    props: ["cocktail"],
    components: {
        "cocktail-name": CocktailName,
        "cocktail-pic": CocktailPic
    },
    methods: {
        
        getKeys(keyName) {
            const cocktailKeys = Object.keys(this.cocktail);
            return cocktailKeys.filter(key => key.includes(keyName));
        },
        
        getIngredients(ingredient) {

            const ingredients = [];

            for (const key of this.getKeys(ingredient)) {
                if (this.cocktail[key] != null) {
                    ingredients.push(this.cocktail[key])
                }
            }
            return ingredients;
        },

        displayForm() {
            this.cocktail.tried = true;
            
        }
    }
}
</script>

<style>

.drink-recipe {
    display: grid;
    grid-template-columns: 1fr 1fr 2fr;
    background-color: rgba(255, 255, 255, 0.892);
    border-radius: 1em;
    box-shadow: 4px 4px 8px rgb(1, 37, 37);
    padding: 5px;
}

.pic {
    width: auto;
    height: 80%;
    justify-self: center;
    align-self: center;
    grid-row: 1/3;
}

.name {
    text-decoration: deeppink underline;
    justify-self: left;
}

#ingredients {
    list-style: none;
    justify-content: left;
}

#method {
    text-align: left;
    margin: 0%;
}

#button {
    justify-self: right;
    margin-right: 1em;
    margin-top: 8px;
}
</style>