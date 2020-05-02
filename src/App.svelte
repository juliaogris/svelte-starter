<script>
	import Card from "./Card.svelte"
	import { items } from "./data.js"
</script>

<div>
	<h1>Fabric Services</h1>
	{#each items as data}
	<Card {data} />
	{/each}
</div>

<style>
	div {
		font-family: "avenir next", avenir, sans-serif;
		margin-right: auto;
		margin-left: auto;
		width: 20rem;
	}
	h1 {
		margin: 0;
		padding: 1rem;
		padding-top: 2rem;
		color: #525252;
		font-size: 3rem;
		font-weight: 500;
	}
	@media screen and (min-width: 30em) {
		div {
			width: 40rem;
		}
	}
	@media screen and (min-width: 60em) {
		div {
			width: 60rem;
		}
	}
	@media screen and (min-width: 80em) {
		div {
			width: 80rem;
		}
	}
</style>
