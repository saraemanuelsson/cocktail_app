<template>
  <div class="drink-recipe">
    <cocktail-name class="name" :cocktail="cocktail"></cocktail-name>
    <div id="button" v-if="!cocktail.tried">
        <button v-on:click="displayForm">I Made This!</button>
        <review-form :cocktail="cocktail"></review-form>
    </div>
    <div id="review" v-else-if="cocktail.tried">
        <p>You scored this {{cocktail.rating}} %</p>
        <p>Notes: {{cocktail.notes}}</p>
    </div>
    <cocktail-pic class="pic" :cocktail="cocktail"></cocktail-pic>
    <div>
        <ul id="ingredients" :key="index" v-for="(measure, index) in getIngredients('Measure')">
            <li>{{measure}}{{getIngredients('Ingredient')[index]}}</li>
        </ul>
    </div>
    <div id="method">
        <h3>Method</h3>
        <p>{{cocktail.strInstructions}}</p>
    </div>
  </div>
</template>

<script>
import CocktailPic from "./CocktailPic";
import CocktailName from "./CocktailName";
import { eventBus } from '../main';
import ReviewForm from "./ReviewForm";

export default {
    name: "cocktail-detail",
    props: ["cocktail"],
    data() {
        return {
            form: {
                isHidden: false
            }
        }
    },
    components: {
        "cocktail-name": CocktailName,
        "cocktail-pic": CocktailPic,
        "review-form": ReviewForm
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
            this.form.isHidden = true;
            eventBus.$emit("cocktail-tried", this.form);
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
    justify-self: end;
    margin-right: 1em;
    margin-top: 8px;
    text-align: right;
}

#review {
    text-align: right;
    margin-right: 1em;
}
</style>