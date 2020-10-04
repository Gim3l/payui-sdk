<script>
	export let width = 50;
	export let height = 50;
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
	<img
		id="barcode"
		src="https://api.qrserver.com/v1/create-qr-code/?data=HelloWorld&size=100x100"
		alt=""
		title="HELLO"
		width={width}
		height={height} />
</main>
