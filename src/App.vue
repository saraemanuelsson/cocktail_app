<template>
  <div id="app">
    <header>
      <img src="./assets/logo.png" alt="Cocktails">
    </header>
    <cocktail-detail></cocktail-detail>
    <cocktail-list></cocktail-list>
  </div>
</template>

<script>
import CocktailDetail from "./components/CocktailDetail";
import CocktailList from "./components/CocktailList";

export default {
  name: 'App',
  components: {
    "cocktail-detail": CocktailDetail,
    "cocktail-list": CocktailList
  },
  data() {
    return {
      cocktails: [],
      selectedCocktail: null
    }
  },
  mounted() {
      fetch("https://www.thecocktaildb.com/api/json/v1/1/search.php?f=a")
      .then(res => res.json())
      .then(cocktailData => this.cocktails = cocktailData)
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
