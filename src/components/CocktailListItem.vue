<template lang="html">
    <li class="drink-card" v-if="cocktail" v-on:click="handleClick">
        <cocktail-pic class="drink-pic" :cocktail="cocktail"></cocktail-pic>
        <cocktail-name class="list-header" :cocktail="cocktail"></cocktail-name>
    </li>
</template>

<script>
import CocktailPic from "./CocktailPic";
import CocktailName from "./CocktailName";
import {eventBus} from '../main.js';
import BackToTop from 'vue-backtotop';

export default {
    name: "cocktail-list-item",
    props: ["cocktail"],
    components: {
        "cocktail-pic": CocktailPic,
        "cocktail-name": CocktailName

    },
    methods: {
        handleClick() {
            this.scrollToTop();
            eventBus.$emit("cocktail-selected", this.cocktail)
        },

        scrollToTop() {
            window.scrollTo(0,0);
        }
    }

}
</script>

<style>

.list-header {
    font-size: 16pt;
    font-weight: lighter;
}

.drink-card {
    display: grid;
    grid-template-columns: 1fr 1fr;
    list-style: none;
    width: 15em;
    height: 7em;
    background-color: rgba(255, 255, 255, 0.742);
    border-radius: 1em;
    align-items: center;
    justify-items: center;
    margin: 6px;
    box-shadow: 4px 4px 8px rgb(1, 37, 37);
}

.drink-card:hover {
    cursor: pointer;
    background-color: rgba(255, 255, 255, 0.892);
    
}

.drink-pic {
    width: 5em;
    height: auto;
}

</style>