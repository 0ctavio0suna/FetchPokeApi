const fetch = require('node-fetch');

// URL de la API de Pokémon
const API_URL = 'https://pokeapi.co/api/v2/pokemon';

// Función principal para obtener y procesar datos de Pokémon
async function getPokemonData() {
    try {
        // Fetch los primeros 10 Pokémon
        const response = await fetch(`${API_URL}?limit=10`);
        const data = await response.json();

        // Imprimir los nombres de los Pokémon con la primera letra en mayúscula
        data.results.forEach(pokemon => {
            console.log(capitalizeFirstLetter(pokemon.name));
        });

        // Fetch la información de un Pokémon específico (por ejemplo, Pikachu)
        const pokemonName = 'pikachu'; // Cambia esto por el nombre del Pokémon que quieras
        const pokemonResponse = await fetch(`${API_URL}/${pokemonName}`);
        const pokemonData = await pokemonResponse.json();

        // Imprimir información del Pokémon específico
        console.log(`Nombre: ${capitalizeFirstLetter(pokemonData.name)}`);
        console.log(`Tipo: ${pokemonData.types.map(type => type.type.name).join(', ')}`);
        console.log(`Habilidades: ${pokemonData.abilities.map(ability => ability.ability.name).join(', ')}`);
        console.log(`Stats:`);
        pokemonData.stats.forEach(stat => {
            console.log(`  ${stat.stat.name}: ${stat.base_stat}`);
        });

    } catch (error) {
        console.error('Error:', error);
    }
}

// Función para capitalizar la primera letra de una cadena
function capitalizeFirstLetter(string) {
    return string.charAt(0).toUpperCase() + string.slice(1);
}

// Ejecutar la función
getPokemonData();
