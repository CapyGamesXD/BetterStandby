<script>
	//@ts-nocheck
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';

	let newUser = true;
	let page = $state(1);
	let accentColour = $state('#8ada93');
	let loading = $state(true);
	let loadingProgress = $state(0);
	let loadingItem = $state('Loading user profile');

	onMount(async () => {
		newUser = (await localStorage.getItem('newUser')) || true;

		loadingProgress = 25;
		loadingItem = 'Setting theme';

		document.body.classList.add('white');

		if (newUser !== true) {
			goto(`/${localStorage.getItem('screen')}`);
		}

		loadingProgress = 100;

		loadingItem = 'Done!';

		setTimeout(() => {
			loading = false;
		}, 500);

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
	{#if loading == false}
		<h1 class="nunito thin subH">Welcome to</h1>
		<h1 class="koulen">Better Standby</h1>
		<div class="divider"></div>
		{#if page === 1}
			<p class="mt-1 font-bold">Please read the following</p>
			<p class="mt-3 text-[14px]">
				Hey! I'm Capy, the developer of Better Standby! 😄 I made it for people who want to use
				things like Apple's StandBy feature but don't have a phone that fully supports it, since
				most phones (including non-pro iPhones) don't have always-on displays. Better Standby
				features screen burn protection, however to take the best possible care of your screen, I
				recommend switching, views, colours, or closing the app occasionally. Screen burn is not
				unique to Better Standby, any app/website can contribute to display wear over prolonged use.
				Enjoy!
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
	{:else}
		<div class="fullcenterdiv">
			<h1>Loading...</h1>
			<p>{loadingItem}</p>
			<div class="progressBG">
				<div class="progressFG" style="width: {loadingProgress}%;"></div>
			</div>
		</div>
	{/if}
</div>

<style>
	.progressBG {
		background-color: black;
		width: 200px;
		height: 20px;
		border-radius: 20px;
	}

	.progressFG {
		background-color: rgb(137, 200, 137);
		height: 20px;
		border-radius: 20px;
		transition: 0.4s ease-in-out;
	}

	.minirow {
		display: flex;
		flex-direction: row;
		gap: 10px;
		align-items: flex-start;
	}

	.centerdiv {
		margin-bottom: 15px;
	}
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
