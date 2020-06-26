<template>
  <div id="app">
    <header>
      <img src="./assets/logo.png" alt="Cocktails">
    </header>
    <!-- <cocktail-detail></cocktail-detail> -->
    <!-- <cocktail-list></cocktail-list> -->
  </div>
</template>

<script>
// import CocktailDetail from "./components/CocktailDetail";
// import CocktailList from "./components/CocktailList";

export default {
  name: 'App',
  components: {
    // "cocktail-detail": CocktailDetail,
    // "cocktail-list": CocktailList
  },
  data() {
    return {
      cocktails: [],
      selectedCocktail: null
    }
  },
  mounted() {
    this.fetchCocktails()

  },

  methods: {
    fetchCocktails() {
      let url = "https://www.thecocktaildb.com/api/json/v1/1/search.php?f="
      const letters = ["a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z"]

      for (const letter of letters) {
        fetch(url + letter)
        .then(res => res.json())
        .then(data => this.cocktails = this.cocktails.concat(data.drinks));
        // .then(data => console.log(data));
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

</style>
