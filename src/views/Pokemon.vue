<template>
  <div>
    <h1>Information about {{ pokemon.name }}</h1>
    <picture>
      <img :src="pokemon.front_default" :alt="pokemon.name" />
    </picture>
    <ul v-for="(move, index) in pokemon.moves" :key="index">
      <li>
        {{ move.move.name }}
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { Component } from "vue-property-decorator";
import Vue from "vue";
import { PokemonModel } from "../models/pokemon.model";

@Component
export default class Pokemon extends Vue {
  pokemon: PokemonModel;

  created(): void {
    this.getPokemon();
  }

  constructor() {
    super();
    this.pokemon = new PokemonModel();
  }

  async getPokemon(): Promise<void> {
    try {
      const res = await fetch(
        `https://pokeapi.co/api/v2/pokemon/${this.$route.params.name}`
      );
      const data = await res.json();

      this.pokemon = data;
      this.pokemon.front_default = data.sprites.front_default;
    } catch (err) {
      console.log(err);
    }
  }
}
</script>

<style></style>
