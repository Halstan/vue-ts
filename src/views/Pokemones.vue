<template>
  <div>
    <h1>{{ message }}</h1>
    <ul>
      <li v-for="(pokemon, index) in pokemones" :key="index">
        <router-link
          :to="{ name: 'Pokemon', params: { name: pokemon.name } }"
          >{{ pokemon.name }}</router-link
        >
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { Component } from "vue-property-decorator";
import Vue from "vue";

@Component
export default class Pokemones extends Vue {
  message = "Pokemones";
  pokemones: unknown[] = [];

  mounted(): void {
    this.getPokemones();
  }

  async getPokemones(): Promise<void> {
    try {
      const res = await fetch(
        "https://pokeapi.co/api/v2/pokemon?limit=20&offset=20"
      );
      const data = await res.json();
      this.pokemones = data.results;
      console.log(this.pokemones);
    } catch (err) {
      console.log(err);
    }
  }
}
</script>
