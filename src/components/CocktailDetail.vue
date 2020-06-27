<template>
  <div class="drink-recipe">
      <cocktail-name></cocktail-name>
      <cocktail-image></cocktail-image>
      <p>Ingredients</p>
      <p>Method</p>
  </div>
</template>

<script>


export default {

}
</script>

<style>

.drink-recipe {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
}

</style>