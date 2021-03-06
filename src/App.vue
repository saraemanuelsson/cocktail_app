<template>
  <div class="app">
    <header>
      <img src="./assets/logo.png" alt="Cocktails" />
    </header>
    <div class="grid">
      <div class="recipe">
        <cocktail-detail v-if="selectedCocktail" :cocktail="selectedCocktail"></cocktail-detail>
      </div>
      <div>
        <h2>Browse Cocktails</h2>
        <search-bar :cocktails="cocktails"></search-bar>
        <cocktail-list class="flex" v-if="displayCocktails" :displayCocktails="displayCocktails"></cocktail-list>
      </div>
      <div>
        <h2>Remake</h2>
        <tried-list :tried="triedCocktails"></tried-list>
      </div>
    </div>
  </div>
</template>

<script>
import { eventBus } from "./main.js";
import CocktailDetail from "./components/CocktailDetail";
import CocktailList from "./components/CocktailList";
import TriedList from "./components/TriedList";
import SearchBar from "./components/SearchBar";

export default {
  name: "App",
  components: {
    "cocktail-detail": CocktailDetail,
    "cocktail-list": CocktailList,
    "tried-list": TriedList,
    "search-bar": SearchBar
  },

  data() {
    return {
      cocktails: [],
      selectedCocktail: null,
      displayCocktails: []
    };
  },

  mounted() {
    this.fetchCocktails();

    eventBus.$on("cocktail-selected", cocktail => (this.selectedCocktail = cocktail));

    eventBus.$on("review-saved", cocktail => (this.selectedCocktail = cocktail));

    eventBus.$on("cocktails-found", cocktails => (this.populateDisplayCocktails(cocktails)));

  },

  computed: {
    triedCocktails: function() {
      return this.cocktails.filter(cocktail => (cocktail.tried));
    }
  },

  methods: {
    fetchCocktails() {
      let url = "https://www.thecocktaildb.com/api/json/v1/1/search.php?f=";
      const letters = ["a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z"];

      for (const letter of letters) {
        fetch(url + letter)
          .then(result => result.json())
          .then(cocktails => {
            this.cocktails = this.cocktails.concat(cocktails.drinks);
            this.cocktails = this.cocktails.map(cocktail => ({
            ...cocktail, tried: false, rating: 0, notes: ""}))
          })
          .then(() => this.shuffle())
          .then(() => this.populateDisplayCocktails(this.cocktails));
      }
    },

    populateDisplayCocktails(cocktails) {
      this.displayCocktails = cocktails
    },

    shuffle() {

      for (let i = this.cocktails.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [this.cocktails[i], this.cocktails[j]] = [this.cocktails[j], this.cocktails[i]];
      }

    }
  }
}

</script>

<style>
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

html {
  background: url("./assets/background.jpg") no-repeat center center fixed;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
  scroll-behavior: smooth;
}

.grid {
  display: grid;
  grid-template-columns: 7fr 3fr;
}

.flex {
  display: flex;
  flex-wrap: wrap;
  justify-content: center; 
}

.recipe {
  grid-column: 1/3;
}

</style>
