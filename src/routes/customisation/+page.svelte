<script>
	//@ts-nocheck
	import { onMount } from 'svelte';
	import { CircleCheck } from 'lucide-svelte';

	let fontChoice = $state();
	let accentColour = $state('#8ada93');

	function pick(item) {
		page = item + 'page';
	}
	let fontSize = $state();
	let originalColour = $state();
	let secondaryFont = $state();
	let page = $state('infopage');

	function saveChanges() {
		localStorage.setItem('screen', page) || 'infopage';
		localStorage.setItem('accentColour', accentColour);
		localStorage.setItem('font', fontChoice);
		localStorage.setItem('secondFont', secondaryFont);
		localStorage.setItem('fontSize', fontSize);
	}
	onMount(() => {
		accentColour = localStorage.getItem('accentColour') || '#8ada93';
		originalColour = accentColour;

		fontChoice = localStorage.getItem('font') || 'nunito';
		fontSize = Number(localStorage.getItem('fontSize')) || 80;
		secondaryFont = localStorage.getItem('secondFont') || 'nunito';
		document.body.classList.remove('black');
		page = localStorage.getItem('screen');
	});
</script>

<div class="centerdiv" style="--accentColour: {accentColour}">
	<a href="/{page}" class="save mt-5 mb-2" onclick={saveChanges}>Save</a>
	<h1 class="koulen">Customisation</h1>
	<div class="divider"></div>
	<a class="accentButton mt-2" href="/settings" onclick={saveChanges}>Settings</a>
	<a href="docs " class="regulara mt-2">About BetterStandby</a>
	<p class="mt-1">Scroll to the bottom to preview</p>
	<div class="row mt-0 mb-4">
		<button
			onclick={() => {
				pick('simple');
			}}
		>
			<div class="bubble">
				<div class="phone thin">19:23</div>
				<div class="stand"></div>
				{#if page === 'simplepage'}
					<CircleCheck class="checkIcon mt-2" color="rgb(0, 0, 0)" />
				{/if}
			</div>
		</button>

		<button
			onclick={() => {
				pick('info');
			}}
		>
			<div class="bubble">
				<div class="phone mt-0 mb-0">
					<div class="minirow">
						<p class=" koulen thin mt-0 mb-0 text-5xl font-normal">19:23</p>
						<div class="leftAlign">
							<div class="minidivider mt-1 mb-2"></div>
							<p class="mt-0 mb-2 text-[10px]/0.5">Sun, 4 Jun</p>
							<p class=" mt-0 mb-2 text-[10px]/0.5 text-green-300">15º</p>

							<div class="minidivider"></div>
						</div>
					</div>
				</div>

				<div class="stand"></div>
				{#if page === 'infopage'}
					<CircleCheck class="checkIcon mt-2" color="rgb(0, 0, 0)" />
				{/if}
			</div>
		</button>
		<button
			onclick={() => {
				pick('colourful');
			}}
		>
			<div class="bubble">
				<div class="phone"><p class="green">19:23</p></div>
				<div class="stand"></div>
				{#if page === 'colourfulpage'}
					<CircleCheck class="checkIcon mt-2" color="rgb(0, 0, 0)" />
				{/if}
			</div>
		</button>
	</div>

	<div class="divider mb-2"></div>
	<p class="mb-2 text-xl">Accent Colour</p>
	{#if accentColour != originalColour}
		<button
			class="accentButton mb-3"
			onclick={() => {
				accentColour = originalColour;
			}}>Undo</button
		>
	{:else}
		<button class="grayedButton mb-3">Undo</button>
	{/if}

	<input type="color" class="colourInput mb-5" bind:value={accentColour} />

	<div class="divider mb-2"></div>

	<p class="mb-2 text-xl">Font:</p>
	<select name="Fonts" bind:value={fontChoice}>
		<option value="nunito">Nunito</option>
		<option value="koulen">Koulen</option>
		<option value="pliant">Pliant</option>
		<option value="montserrat">Montserrat</option>
		<option value="oswald">Oswald</option>
		<option value="robotoslab">Roboto Slab</option>
		<option value="pixelify">Pixelify Sans</option>
	</select>
	<p class="mt-2 mb-1 text-xl">Secondary Font:</p>
	<select name="Fonts" bind:value={secondaryFont}>
		<option value="nunito">Nunito</option>
		<option value="koulen">Koulen</option>
		<option value="pliant">Pliant</option>
		<option value="montserrat">Montserrat</option>
		<option value="oswald">Oswald</option>
		<option value="robotoslab">Roboto Slab</option>
		<option value="pixelify">Pixelify Sans</option>
	</select>

	<p class="mt-2 mb-1 text-xl">Main font size:</p>
	<p>{Math.floor(((fontSize - 50) / 50) * 100)}</p>
	<input type="range" step="5" min="50" max="100" class="mb-2" bind:value={fontSize} />
	<div class="divider mb-2"></div>

	<p class="mb-2 text-xl">Preview</p>
	<div class="preview mb-4" style="--fontSize: {fontSize}">
		<p
			class="previewText mb-0 {fontChoice}"
			style="font-size: {fontSize / 1.4}px; margin: 0; line-height: 1"
		>
			White Text
		</p>

		<p class="colourfulText mt-2 {secondaryFont}">Colourful Text</p>
	</div>
</div>

<style>
	.regulara {
		width: auto;
		font-size: 13px;
	}
	.save {
		background-color: var(--accentColour);
		padding: 3px 10px 5px 10px;
		width: 50px;
		font-size: 13px;
		border-radius: none;
		box-shadow: inset 0px -5px 0px 0px rgba(0, 0, 0, 0.163);
		border-radius: 20px;
		display: flex;
		color: rgb(0, 0, 0);
		justify-content: center;
		align-items: center;
		color: contrast-color(var(--accentColour));
	}
	select {
		outline: none;
	}
	.leftAlign {
		display: flex;
		align-items: flex-start;
		flex-direction: column;
		width: 100%;
	}
	.minirow {
		display: flex;
		flex-direction: row;
		gap: 10px;
		align-items: flex-start;
	}

	.accentButton {
		background-color: var(--accentColour);

		color: contrast-color(var(--accentColour));

		width: 100px;
		height: 30px;

		font-size: 13px;
		border-radius: 15px;
		outline: none;
		border: none;
		padding: 3px 10px 5px 10px;

		box-shadow: inset 0px -5px 0px 0px rgba(0, 0, 0, 0.163);
	}

	.grayedButton {
		background-color: rgb(73, 73, 73);
		color: contrast-color(var(--accentColour));
		width: 100px;
		height: 30px;
		font-size: 13px;
		border-radius: 15px;
		outline: none;
		border: none;
		padding: 3px 10px 5px 10px;
		box-shadow: inset 0px -5px 0px 0px rgba(0, 0, 0, 0.163);
	}

	.preview {
		border: 2px solid var(--accentColour);

		border-radius: 20px;
		width: 400px;
		height: 200px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		background-color: black;
	}

	.previewText {
		color: white;
		will-change: font-size;
		width: 100%;
	}

	.colourfulText {
		color: var(--accentColour);
	}
	.green {
		color: rgb(147, 207, 147);
	}
	.minidivider {
		width: 50px;
		height: 4px;
		background-color: rgb(53, 53, 53);
		border-radius: 20px;
	}

	a {
		color: contrast-color(var(--accentColour));

		background-color: var(--accentColour);
		width: 60px;
		height: 30px;
		border-radius: 30px;
		display: flex;
		padding: 3px 10px 5px 10px;
		box-shadow: inset 0px -5px 0px 0px rgba(0, 0, 0, 0.163);
		justify-content: center;
		align-items: center;
	}

	.koulen {
		font-size: 30px;
	}
</style>
