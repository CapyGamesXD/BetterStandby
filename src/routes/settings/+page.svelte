<script>
	//@ts-nocheck
	import { goto } from '$app/navigation';
	import { page } from '$app/state';

	import { onMount } from 'svelte';

	let accentColour = $state('#8ada93');

	let lat = $state('');
	let lon = $state('');
	let hiddenLocation = $state(true);
	onMount(() => {
		accentColour = localStorage.getItem('accentColour') || '#8ada93';
		lat = localStorage.getItem('lat');
		lon = localStorage.getItem('lon');
		document.body.style.backgroundColor = '#8fc4e1';
		return () => {
			document.body.style.backgroundColor = '#FFFFFF';
		};
	});

	//GPS location fetching! :D
	async function fetchLocation() {
		if ('geolocation' in navigator) {
			navigator.geolocation.getCurrentPosition(
				(position) => {
					lat = position.coords.latitude.toFixed(5);
					lon = position.coords.longitude.toFixed(5);
				},
				(error) => {
					console.error(error);
					if (error.code === 1) {
						alert('Location permission denied, unable to fetch.');
					} else if (error.code === 2) {
						alert('Position unavailable. Please check device.');
					} else if (error.code === 3) {
						alert('Fetch timeout, please try again later.');
					} else {
						alert('Unexpected error, please try again later.');
					}
				}
			);
		} else {
			alert('This browser does not support automatic fetch.');
		}
	}

	function saveChanges() {
		if (lat && lon) {
			localStorage.setItem('lat', lat);
			localStorage.setItem('lon', lon);
		} else {
			alert('Please enter a valid location');
		}
	}
</script>

<div style="--accentColour: {accentColour}">
	<div class="fullcenterdiv" style="--accentColour: {accentColour}">
		<div class="box">
			<h1 class="koulen">Settings</h1>
			<a href="/customisation" class="save" onclick={saveChanges}>Save</a>

			<p class="latlon mt-2">Latitude:</p>
			{#if hiddenLocation === true}
				<div class="hiddenInput">Hidden</div>
				<p class="latlon mt-1">Longitude:</p>
				<div class="hiddenInput">Hidden</div>
			{:else}
				<input bind:value={lat} placeholder="E.g, 48.8584" />
				<p class="latlon mt-1">Longitude:</p>
				<input bind:value={lon} placeholder="E.g, 2.2945" />
			{/if}

			<div class="row mt-2">
				<p class="hide">Hide location</p>
				<input type="checkbox" class="checkbox" bind:checked={hiddenLocation} />
			</div>

			<button onclick={fetchLocation} class="mt-2">Fetch Automatically</button>
			<p class="mt-2 mb-2">This data is stored on-device, and is only used for weather fetching.</p>

			<div class="divider mt-1 mb-2"></div>
			<div class="dangerZone">
				<button
					class="coolButton mt-1"
					onclick={() => {
						localStorage.clear();
						goto('/');
					}}>Clear All Storage</button
				>
				<p class="mt-2">This includes location, tutorial, and font styling.</p>
			</div>
		</div>
	</div>
</div>

<style>
	.hide {
		font-size: 15px;
		width: auto;
	}
	.latlon {
		font-size: 20px;
		font-weight: 500;
	}
	.box {
		width: 300px;
		background-color: rgb(219, 219, 219);
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 20px;
		height: 380px;
		border-radius: 20px;
	}
	input[type='checkbox'] {
		border: none;
		width: 15px;
		margin: none;
	}
	.dangerZone {
		background-color: rgb(219, 113, 113);
		padding: 5px 50px 10px 50px;
		border-radius: 20px;
		box-shadow: inset 0px -5px 0px 0px rgba(0, 0, 0, 0.163);
		margin-bottom: 10px;
		display: flex;
		flex-direction: column;
		align-items: center;
		height: 80px;
		justify-content: center;
	}

	p {
		width: 150px;
		font-size: 9px;
		font-family: 'Montserrat', sans-serif;
	}

	button {
		width: 150px;
		height: 30px;
		background-color: rgb(63, 63, 63);
		font-size: 13px;
		border-radius: 15px;
		outline: none;
		border: none;
		padding: 3px 10px 5px 10px;
		color: white;
		box-shadow: inset 0px -5px 0px 0px rgba(0, 0, 0, 0.163);
	}

	@media (hover: hover) {
		button:hover {
			transform: scale(1.1);
		}
	}
	.coolButton {
		background-color: rgb(230, 88, 88);
		width: 130px;
		height: 30px;
		border-radius: 15px;
		font-size: 13px;

		color: contrast-color(var(--accentColour));
	}
	@media (hover: hover) {
		.coolButton:hover {
			background-color: red;
		}
	}

	input,
	.hiddenInput {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		text-align: center;
		background-color: rgb(184, 184, 184);
		border-radius: 8px;
		outline: none;
		height: 20px;
		width: 150px;
		font-size: 12px;
	}

	a {
		background-color: var(--accentColour);
		padding: 3px 10px 5px 10px;

		box-shadow: inset 0px -5px 0px 0px rgba(0, 0, 0, 0.163);

		display: flex;
		color: rgb(0, 0, 0);
		justify-content: center;
		align-items: center;
		color: contrast-color(var(--accentColour));
	}

	.save {
		background-color: var(--accentColour);
		padding: 0px 10px 2px 10px;
		width: 50px;
		font-size: 13px;
		border-radius: none;
		box-shadow: inset 0px -2px 0px 0px rgba(0, 0, 0, 0.163);
		border-radius: 20px;
		display: flex;
		color: rgb(0, 0, 0);
		justify-content: center;
		align-items: center;
		color: contrast-color(var(--accentColour));
	}

	.koulen {
		color: rgb(0, 0, 0);
		font-size: 14px;
	}
</style>
