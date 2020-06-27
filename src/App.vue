<template>
  <div id="app">
    <header>
      <img src="./assets/logo.png" alt="Cocktails" />
    </header>
    <div class="grid">
      <div>
        <cocktail-list class="flex" :cocktails="cocktails"></cocktail-list>
      </div>
      <div>
        <cocktail-detail v-if="selectedCocktail" :cocktail="selectedCocktail"></cocktail-detail>
      </div>
    </div>
  </div>
</template>

<script>
import CocktailDetail from "./components/CocktailDetail";
import CocktailList from "./components/CocktailList";

export default {
  name: "App",
  components: {
    "cocktail-detail": CocktailDetail,
    "cocktail-list": CocktailList
  },
  data() {
    return {
      cocktails: [],
      selectedCocktail: null
    };
  },
  mounted() {
    this.fetchCocktails()

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
          .then(() => this.shuffle());
      }
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
#app {
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
</style>
