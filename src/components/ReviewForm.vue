<template>
  <form v-if="isHidden" id="form" v-on:submit.prevent="handleSubmit">
      <label for="rating">Score</label>
      <input type="number" min="0" max="100" id="rating" placeholder="0" v-model="rating" value="rating">%</input>
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
            "isHidden": false
        }
    },
    methods: {
        handleSubmit() {
            this.cocktail.tried = true;
            this.cocktail.rating = this.rating;
            this.cocktail.notes = this.notes;
            this["rating"] = 0;
            this["notes"] = "";
            this["isHidden"] = false;
            eventBus.$emit("review-saved", this.cocktail);
        }
    },
    mounted() {
        eventBus.$on("cocktail-tried", form => (this.isHidden = form))
    }

}
</script>

<style>

</style>