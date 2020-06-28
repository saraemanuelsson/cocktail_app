<template>
  <form v-if="isHidden" id="form" v-on:submit.prevent="handleSubmit">
      <label for="rating">Score</label>
      <input type="number" min="0" max="100" id="rating" v-model="rating" value="rating">%
      <input type="text" placeholder="Notes for next time" v-model="notes" value="notes">
      <input type="submit" value="Save">
  </form>
</template>

<script>
import { eventBus } from '../main';

export default {
    name: "review-form",
    props: ["cocktail"],
    data() {
        return {
            "rating": 0,
            "notes": "",
            "isHidden": false,
            editedCocktail: {}
        }
    },
    methods: {
        handleSubmit() {
            this.editedCocktail = this.cocktail;
            this.editedCocktail.tried = true;
            this.editedCocktail.rating = this.rating;
            this.editedCocktail.notes = this.notes;
            this["rating"] = 0;
            this["notes"] = "";
            this["isHidden"] = false;
            eventBus.$emit("review-saved", this.editedCocktail);
        }
    },
    mounted() {
        eventBus.$on("cocktail-tried", form => (this.isHidden = form))
    }

}
</script>

<style>

</style>