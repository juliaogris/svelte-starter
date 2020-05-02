<script>
	export let labels
	export let data
	export let startTime
	export let endTime

	import { timelineLabels, stateAttr } from "./const.js"

	$: state = data[data.length - 1][1]

	$: label = labels[state]
	$: color = stateAttr.colors[state]
	$: fontWeight = stateAttr.fontWeights[state]

	$: d = [...data, [endTime, -1]]
	$: start = new Date(startTime).getTime()
	$: end = new Date(endTime).getTime()

	function rectProps(i) {
		const iStart = new Date(d[i][0]).getTime()
		const iEnd = new Date(d[i + 1][0]).getTime()

		const x = (iStart - start) / (end - start)
		const endX = (iEnd - start) / (end - start)
		const width = endX - x
		const color = stateAttr.colors[d[i][1]]
		return { x, width, fill: color, stroke: color }
	}

	function handleMouseover(i) {
		return e => {
			e.target.style.fill = stateAttr.hoverColors[d[i][1]]
			e.target.style.transform = "translateY(-0.2px) scaleY(1.4)"
			e.target.style.strokeWidth = "0"
		}
	}

	function handleMouseout(i) {
		return e => {
			e.target.style.fill = stateAttr.colors[d[i][1]]
			e.target.style.transform = ""
			e.target.style.strokeWidth = "0"
		}
	}
</script>

<div>
	<h4 style="color: {color}; font-weight: {fontWeight}">
		{label}
		<span style="border-color: {color}" />
	</h4>
	<svg viewBox="0 0 1 1" preserveAspectRatio="none">
		{#each data as _, i}
		<rect
			{...rectProps(i)}
			y=".2"
			height=".6"
			vector-effect="non-scaling-stroke"
			on:mouseover="{handleMouseover(i)}"
			on:mouseout="{handleMouseout(i)}"
		/>
		{/each}
	</svg>
</div>

<style>
	div {
		width: 100%;
	}
	h4 {
		margin: 0;
		padding-right: 0.5rem;
		position: relative;
		font-size: 1.25rem;
		text-align: right;
	}
	svg {
		width: 100%;
		height: 1.5rem;
		stroke-width: 0;
	}
	span {
		width: 0.25rem;
		position: absolute;
		height: 1.5rem;
		right: 0;
		top: 0.9rem;
		font-weight: bold;
		border-top: 2px solid;
		border-right: 2px solid;
		z-index: -1;
	}
</style>
