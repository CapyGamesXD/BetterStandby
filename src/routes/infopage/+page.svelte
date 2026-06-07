<script>
	//@ts-nocheck

	import { onMount } from 'svelte';

	let accentColour = $state('#8ada93');
	let font = $state();
	let secondaryFont = $state();
	let fontSize = $state();

	onMount(async () => {
		font = localStorage.getItem('font') || 'nunito';
		secondaryFont = localStorage.getItem('secondFont') || 'nunito';
		accentColour = localStorage.getItem('accentColour') || '#8ada93';
		fontSize = localStorage.getItem('fontSize') || 85;
		lat = localStorage.getItem('lat');
		lon = localStorage.getItem('lon');

		getWeather();
		document.body.classList.add('black');
		return () => {
			document.body.classList.remove('black');
			clearInterval(dateInterval);
			clearInterval(weatherInterval);
		};
	});
	let lat = $state();
	let lon = $state();
	let temp = $state('Loading...');

	async function getWeather() {
		const url = `https://api.open-meteo.com/v1/forecast?latitude=${lat}&longitude=${lon}&current=temperature_2m`;
		try {
			const apiResponse = await fetch(url);

			const result = await apiResponse.json();
			temp = result.current.temperature_2m.toFixed(1);
			console.log(temp);
		} catch {
			console.log('API error');
		}
	}

	let date = new Date();
	let minutes = $state(date.getMinutes().toString());
	let hours = $state(date.getHours().toString());
	let day = $state(date.getDay());
	let monthDate = $state(date.getDate());
	let month = $state(date.getMonth());
	const days = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'];
	const months = [
		'Jan',
		'Feb',
		'Mar',
		'Apr',
		'May',
		'Jun',
		'Jul',
		'Aug',
		'Sep',
		'Oct',
		'Nov',
		'Dec'
	];

	const weatherInterval = setInterval(() => {
		getWeather();
	}, 1200000);

	const dateInterval = setInterval(() => {
		date = new Date();
		minutes = date.getMinutes().toString();
		hours = date.getHours().toString();
		day = date.getDay();
		monthDate = date.getDate();
		month = date.getMonth();
	}, 1000);
</script>

<a href="customisation">
	<div class="antiBurn">
		<div class="fullcenterdiv" style="--accent: {accentColour}">
			<div class="row">
				<h1
					style="font-size: {fontSize / 3.5}vw; margin: 0; line-height: 1"
					class="hugeText {font}"
				>
					{hours.padStart(2, '0')}:{minutes.padStart(2, '0')}
				</h1>

				<div class="top">
					<div class="divider mt-4"></div>
					<p class="{secondaryFont} size">{days[day]}, {monthDate} {months[month]}</p>
					{#if lat === '' || lat === undefined || lat === null}
						<p class="{secondaryFont} font-s">Couldn't get location. Please enter in settings.</p>
						<div class=" divider mt-3"></div>
					{:else}
						<p class="white size {secondaryFont}">{temp}º</p>
						<div class=" divider mt-3"></div>
					{/if}
				</div>
			</div>
		</div>
	</div>
</a>

<style>
	.size {
		font-size: 4vw;
	}
	.divider {
		background-color: rgb(45, 45, 45);
		width: 17vw;
	}
	.white {
		color: white;
	}
	.hugeText {
		font-weight: 800;
		color: white;
		line-height: 0.9;
		font-size: 25vw;
	}

	p {
		color: var(--accent);

		margin-top: 15px;
		line-height: 1;
	}

	.row {
		display: flex;
		align-items: flex-start;
	}
	* {
		text-align: left;
	}
</style>
