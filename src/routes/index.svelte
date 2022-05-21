<script context="module">
	export async function load({ params }) {
		const url = `https://pokeapi.co/api/v2/pokemon?limit=898`;
		const res = await fetch(url);
		const data = await res.json();
		const loadedPokemon = data.results.map((data, index) => {
			return {
				name: data.name,
				id: index + 1,
				image: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/back/${
					index + 1
				}.png`
			};
		});
		return {
			props: {
				pokemon: loadedPokemon
			}
		};
		// pokemon.set(loadedPokemon);
	}
</script>

<script>
	import PokemanCard from './../components/pokemanCard.svelte';
	// import { pokemon } from './../stores/pokestore.js';

	export let pokemon;

	let searchTerm = '';
	let filteredPokemon = [];

	$: {
		console.log('searchTerm', searchTerm);
		if (searchTerm) {
			filteredPokemon = pokemon.filter((pokeman) =>
				pokeman.name.toLowerCase().includes(searchTerm.toLowerCase())
			);
		} else {
			filteredPokemon = [...pokemon];
		}
	}
	console.log('pokemon', pokemon);
	console.log('Hello', 'jihoo');
</script>

<svelte:head>
	<title>지우 포켓몬도감 Pokdex</title>
</svelte:head>
<h1 class="text-4xl text-center my-8 uppercase">지우 Pokedex (포켓몬 도감)</h1>

<input
	class="w-full rounded-md text-lg p-4 border-2 border-gray-200"
	type="text"
	placeholder="Search Pokemon"
	bind:value={searchTerm}
/>

<div class="py-4 grid gap-4 md:grid-cols-2 grid-cols-1">
	{#each filteredPokemon as pokeman}
		<PokemanCard {pokeman} />
	{/each}
</div>
