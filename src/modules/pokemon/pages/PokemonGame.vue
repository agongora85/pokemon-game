<template>
    <section v-if="isLoading || randomPokemon.id === null " class="flex flex-col justify-center items-center w-screen h-screen">
        <h1 class="text-3xl">Espere por favor</h1>
        <h3 class="animate-pulse">Cargando Pokémons</h3>
    </section>

    <section v-else class="flex flex-col justify-center items-center w-screen h-screen">
        <h1 class="mt-5">¿Quién es este Pokémon?</h1>
        <h3 class="capitalize">{{  gameStatus }}</h3>
        <div class="h-20">
            <button v-if="gameStatus != GameStatus.Playing" 
                @click="getNextRound(4)"
                class="bg-blue-500 text-white p-2 rounded-md hover:bg-blue-700 transition-all">
                ¿Jugar de nuevo?
            </button>
        </div>
        <!-- Pokémon Picture -->
        <PokemonPicture :pokemon-id="randomPokemon.id" :show-pokemon="gameStatus != GameStatus.Playing"/>
        <!-- Pokémon Options-->
         <PokemonOptions 
         :options="options" 
         :block-selection="gameStatus != GameStatus.Playing"
         :correct-answer="randomPokemon.id"
         @selected-option="checkAnswer"/>
    </section>


</template>

<script lang="ts" setup>
import PokemonOptions from '@/components/PokemonOptions.vue';
import PokemonPicture from '../components/PokemonPicture.vue';
import { usePokemonGame } from '../composables/usePokemonGame.ts';
import { GameStatus } from '../interfaces/game-status-enum.ts';
const { randomPokemon, isLoading, gameStatus, pokemonOptions:options, checkAnswer, getNextRound } = usePokemonGame();
const onSelectedOption = (value: number)=>{
    console.log({ value });
};
</script>

<style scope>
</style>