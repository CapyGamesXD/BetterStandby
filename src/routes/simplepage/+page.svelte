<script>
	//@ts-nocheck
	import { onMount } from 'svelte';

	let font = $state();
	let fontSize = $state();

	onMount(async () => {
		font = localStorage.getItem('font') || 'nunito';

		fontSize = localStorage.getItem('fontSize') || 85;
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
		<div class="fullcenterdiv">
			<h1
				class="hugeText thin {font}"
				style="font-size: {fontSize / 3}vw; margin: 0; line-height: 1"
			>
				{hours.padStart(2, '0')}:{minutes.padStart(2, '0')}
			</h1>
		</div>
	</div>
</a>

<style>
	.hugeText {
		color: white;
		font-weight: 100;
	}
</style>
