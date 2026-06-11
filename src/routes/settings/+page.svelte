<script>
	//@ts-nocheck
	import { goto } from '$app/navigation';

	import { onMount } from 'svelte';

	let accentColour = $state('#8ada93');

	let lat = $state();
	let lon = $state();
	onMount(() => {
		accentColour = localStorage.getItem('accentColour') || '#8ada93';
		lat = localStorage.getItem('lat');
		lon = localStorage.getItem('lon');
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
					alert(error.code, error.message);
				}
			);
		} else {
			alert('This browser does not support automatic fetch.');
		}
	}

	function saveChanges() {
		if (lat !== undefined && lon !== undefined) {
			localStorage.setItem('lat', lat);
			localStorage.setItem('lon', lon);
		}
	}
</script>

<div class="centerdiv" style="--accentColour: {accentColour}">
	<a href="/customisation" class="mb-2">Cancel</a>
	<a href="/customisation" class="mt-1 mb-2" onclick={saveChanges}>Save</a>
	<h1 class="koulen">Settings</h1>
	<div class="divider"></div>

	<p class="mt-2 text-xl">Latitude:</p>
	<input bind:value={lat} placeholder="E.g, 48.8584" />
	<p class="mt-2 text-xl">Longitude:</p>
	<input bind:value={lon} placeholder="E.g, 2.2945" />
	<button onclick={fetchLocation} class="mt-2">Fetch Automatically</button>
	<p class="mt-2">This data is stored on-device, and is only used for weather fetching.</p>
	<div class="divider mt-1 mb-2"></div>
	<button
		class="coolButton mt-1"
		onclick={() => {
			localStorage.clear();
			goto('/');
		}}>Clear All Storage</button
	>
	<p class="mt-2">This includes location, tutorial, and font styling.</p>
	<div class="divider mt-1 mb-1"></div>
</div>

<style>
	button {
		width: 200px;
		height: 40px;
		background-color: rgb(127, 114, 199);
		color: white;
		border-radius: 30px;
		outline: none;
		border: none;
		padding: 3px 10px 5px 10px;

		box-shadow: inset 0px -5px 0px 0px rgba(0, 0, 0, 0.163);
	}

	button:hover {
		transform: scale(1.1);
	}
	.coolButton {
		background-color: var(--accentColour);
		width: 150px;
		height: 30px;
		border-radius: 30px;
		color: black;
	}
	@media (hover: hover) {
		.coolButton:hover {
			background-color: red;
		}
	}

	input {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		text-align: center;
		background-color: rgb(209, 209, 209);
		border-radius: 20px;
		outline: none;
	}

	a {
		background-color: var(--accentColour);
		padding: 3px 10px 5px 10px;

		box-shadow: inset 0px -5px 0px 0px rgba(0, 0, 0, 0.163);
		border-radius: 30px;
		display: flex;
		color: rgb(0, 0, 0);
		justify-content: center;
		align-items: center;
	}
</style>
