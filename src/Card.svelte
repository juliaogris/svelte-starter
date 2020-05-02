<script>
	export let data
	export let big = false

	import Timeline from "./Timeline.svelte"
	import { timelineLabels, stateAttr } from "./const.js"

	function props(type) {
		return {
			labels: timelineLabels[type],
			data: data[type],
			startTime: data.startTime,
			endTime: data.endTime
		}
	}
	const available = props("available")
	const secure = props("secure")
	const compliant = props("compliant")
	$: color = stateAttr.colors[data.state]
</script>

<div class:big>
	<section>
		<h3 style="background-color: {color}" on:click="{() => {big = !big}}">
			{#if big} ← {/if} {data.name}
		</h3>
		<p>
			<Timeline {...available} />
			<Timeline {...secure} />
			<Timeline {...compliant} />
		</p>
	</section>
</div>

<style>
	div {
		width: 20rem;
		display: inline-block;
		margin: 0;
		transition: all 400ms ease-in-out;
	}
	.big {
		width: 100%;
		display: block;
	}
	section {
		margin: 1rem;
		display: block;
		border: 0.125rem solid dimgrey;
		border-radius: 0.25rem;
		box-shadow: 0px 0px 4px 2px rgba(0, 0, 0, 0.2);
	}
	h3 {
		margin: 0;
		padding: 1rem 2rem;
		display: block;
		text-align: center;
		font-weight: 600;
		letter-spacing: 0.1em;
		border-bottom: 2px solid dimgrey;
		color: white;
		font-size: 1.5rem;
	}
	h3:hover {
		cursor: pointer;
		text-decoration: underline;
	}
	p {
		padding: 0.5rem 1rem;
		line-height: 1.5;
	}
</style>
