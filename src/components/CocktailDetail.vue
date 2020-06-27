<template>
  <div class="drink-recipe">
    <cocktail-pic class="pic" :cocktail="cocktail"></cocktail-pic>
    <div>
        <cocktail-name class="name" :cocktail="cocktail"></cocktail-name>
        <ul v-for="(measure, index) in getIngredients('Measure')">
            <li>{{measure}}{{getIngredients('Ingredient')[index]}}</li>
        </ul>
    </div>
    <p class="method">{{cocktail.strInstructions}}</p>
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
}

.pic {
    height: 80%;
    width: auto;
    justify-self: center;
    align-self: center;
}

.name {
    text-decoration: deeppink underline;
}

.ingredients {

}

.method {
    grid-column: ;
}
</style>