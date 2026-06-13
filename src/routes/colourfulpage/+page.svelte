<script>
	//@ts-nocheck
	import { onMount } from 'svelte';

	let accentColour = $state('#8ada93');
	let font = $state();
	let fontSize = $state();
	onMount(async () => {
		font = localStorage.getItem('font') || 'nunito';
		accentColour = localStorage.getItem('accentColour') || '#8ada93';
		fontSize = localStorage.getItem('fontSize');

		document.body.classList.add('black');
		return () => {
			document.body.classList.remove('black');
		};
	});

	let date = new Date();
	let minutes = $state(date.getMinutes().toString());
	let hours = $state(date.getHours().toString());

	const dateInterval = setInterval(() => {
		date = new Date();
		minutes = date.getMinutes().toString();
		hours = date.getHours().toString();
	}, 1000);
</script>

<a href="customisation">
	<div class="antiBurn">
		<div class="fullcenterdiv" style="--accent: {accentColour}">
			<h1 class="hugeText {font}" style="font-size: {fontSize / 3}vw; margin: 0; line-height: 1">
				{hours.padStart(2, '0')}:{minutes.padStart(2, '0')}
			</h1>
		</div>
	</div>
</a>

<style>
	.fullcenterdiv {
		overflow: hidden;
	}
	.hugeText {
		color: var(--accent);
		font-weight: 600;
		font-size: 50vh;
	}
</style>
