<script>
	//@ts-nocheck
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';

	let newUser = true;
	let page = $state(1);
	let accentColour = $state('#8ada93');
	onMount(async () => {
		newUser = (await localStorage.getItem('newUser')) || true;
		if (newUser !== true) {
			console.log('User is not new!');
			goto(`/${localStorage.getItem('screen')}`);
		}

		document.body.classList.add('white');
		return () => {
			document.body.classList.remove('white');
		};
	});

	function accept() {
		localStorage.setItem('newUser', false);
		localStorage.setItem('accentColour', accentColour);
		goto(`/${localStorage.getItem('screen')}`);
	}

	function pick(item) {
		localStorage.setItem('screen', item + 'page');
		page += 1;
	}
</script>

<div class="centerdiv" style="--accent: {accentColour}">
	<h1 class="nunito thin subH">Welcome to</h1>
	<h1 class="koulen">Better Standby</h1>
	<div class="divider"></div>
	{#if page === 1}
		<p class="mt-1 font-bold">Please read the following</p>
		<p class="mt-3 text-[14px]">
			Hey! I'm Capy, the developer of Better Standby! 😄 I made it for people who want to use things
			like Apple's StandBy feature but don't have a phone that fully supports it, since most phones
			(including non-pro iPhones) don't have always-on displays. Better Standby features screen burn
			protection, however to take the best possible care of your screen, I recommend switching,
			views, colours, or closing the app occasionally. Screen burn is not unique to Better Standby,
			any app/website can contribute to display wear over prolonged use. Enjoy!
		</p>
		<button
			onclick={() => {
				page++;
			}}
			class="greenBG button3d mt-2">Accept and Continue</button
		>
	{:else if page === 2}
		<div class="slideAnim">
			<p class="mt-2 mb-0">Great! Let's choose a theme. You can change this later.</p>
			<div class="row mt-0 mb-4">
				<button
					onclick={() => {
						pick('simple');
					}}
				>
					<div class="bubble">
						<div class="phone thin">19:23</div>
						<div class="stand"></div>
					</div>
				</button>

				<button
					onclick={() => {
						pick('info');
					}}
				>
					<div class="bubble">
						<div class="phone mt-0 mb-0">
							<p class=" mt-0 mb-0">19:23</p>
							<p class=" mt-0 mb-2 text-[10px]/0.5 text-green-300">15º</p>
						</div>

						<div class="stand"></div>
					</div>
				</button>
				<button
					onclick={() => {
						pick('colourful');
					}}
				>
					<div class="bubble">
						<div class="phone"><p class=" text-green-300">19:23</p></div>
						<div class="stand"></div>
					</div>
				</button>
			</div>
		</div>
	{:else if page === 3}
		<div class="slideAnim">
			<p class="mt-2">Great choice! Now let's choose an accent colour!</p>
			<input type="color" class="colourInput mt-2" bind:value={accentColour} />
			<button
				onclick={() => {
					page++;
				}}
				class="changeyButton mt-2">Next</button
			>
		</div>
	{:else if page === 4}
		<div class="slideAnim">
			<p class="mt-2">
				Almost done! <br /> If you want to customise further, all you need to do is tap on the time!
			</p>
			<button class="changeyButton mt-2" onclick={accept}> Done! </button>
		</div>
	{/if}
</div>

<style>
	.changeyButton {
		background-color: var(--accent);
		width: 250px;
		height: 50px;
		border-radius: 50px;
		font-size: 20px;
		font-weight: 600;
		box-shadow: inset 0px -5px 0px 0px rgba(0, 0, 0, 0.163);
	}

	.bubble {
		width: 200px;
		height: 200px;
		background-color: #d9d9d9;
		border-radius: 20px;
		margin-top: 10px;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		transition: 0.4s;
	}

	.changeyButton:hover,
	.greenBG:hover {
		transform: scale(1.1);
	}
</style>
