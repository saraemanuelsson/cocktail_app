<template lang="html">
    <div>
        <h2>Remake:</h2>
        <div id="tried-list">
            <ul  v-for="(cocktail, index) of tried" >
                <li class="list-item"  v-on:click="handleClick(cocktail)">{{cocktail.strDrink}}</li>
            </ul>
        </div>
    </div>
</template>

<script>
import {eventBus} from "../main.js"

export default {
    name: "tried-list",
    props: ["tried"],
    methods: {
        handleClick(cocktail) {
            eventBus.$emit("cocktail-selected", cocktail)
        }
    }

}
</script>

<style>

#tried-list {
    margin-top: 27px;
    background-color: rgba(255, 255, 255, 0.742);
    border-radius: 1em;
    box-shadow: 4px 4px 8px rgb(1, 37, 37);
    font-size: 16pt;
    text-decoration: underline deeppink;
}

.list-item {
    list-style: none;
}

.list-item:hover {
    cursor: pointer;
}

</style>