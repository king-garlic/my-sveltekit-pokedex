<script context="module">
	export async function load({ params }) {
		const id = params.id;
		console.log('id', id);
		const url = `https://pokeapi.co/api/v2/pokemon/${id}`;
		const res = await fetch(url);
		const pokeman = await res.json();
		console.log('pokeman', pokeman);

		return {
			props: { pokeman }
		};
	}
</script>

<script>
	export let pokeman;
	const type = pokeman.types[0].type.name;
</script>

<div class="flex flex-col items-center">
	<h1 class="text-4xl text-center my-8 uppercase">{pokeman.name}</h1>
	<p>
		Type: <strong>{type}</strong>
		| Height: <strong>{pokeman.height}</strong>
		| Weight: <strong>{pokeman.weight}</strong>
	</p>
	<img
		class="card-image"
		src={pokeman.sprites['front_default']}
		alt={pokeman.name}
		height={20 * pokeman.height}
	/>
</div>
