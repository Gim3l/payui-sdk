<script>
	import { createEventDispatcher } from 'svelte';
	import { get_current_component } from 'svelte/internal';
	const component = get_current_component();
	const svelteDispatch = createEventDispatcher();
	const dispatch = (name, detail) => {
		svelteDispatch(name, detail);
		component.dispatchEvent && component.dispatchEvent(new CustomEvent(name, { detail }));
	};

	export let width = 50;
	export let height = 50;
	export let onComplete;
	const fetchImage = (async () => {
		const response = await fetch('https://dog.ceo/api/breeds/image/random').then((res) => {
			dispatch('complete', res);

			return res;
		});

		return await response.json();
	})();
</script>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>

<svelte:options tag="payui-sdk" immutable={true} />
<main>
	Helo
	{#await fetchImage}
		<p>...waiting</p>
	{:then data}
		<img src={data.message} alt="Dog image" />
	{:catch error}
		<p>An error occurred!</p>
	{/await}
	<!-- <img
		id="barcode"
		src="https://api.qrserver.com/v1/create-qr-code/?data=HelloWorld&size=100x100"
		alt=""
		title="HELLO"
		{width}
		{height} /> -->
</main>
