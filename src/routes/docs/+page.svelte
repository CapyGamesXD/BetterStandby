<script>
	//@ts-nocheck
	import { onMount } from 'svelte';

	let accentColour = $state('#8ada93');
	let font = $state();

	onMount(async () => {
		font = localStorage.getItem('font') || 'nunito';
		accentColour = localStorage.getItem('accentColour') || '#8ada93';

		document.body.classList.remove('black');
	});
</script>

<div class="centerdiv mb-3" style="--accentColour: {accentColour}">
	<a href="/customisation" class="fancya mt-4 mb-2">Exit</a>
	<h1 class="koulen mt-2">About BetterStandby:</h1>
	<h2 class="koulen">The idea:</h2>
	<p>
		The idea for BetterStandby is to give phones without Apple's always-on function a nice-looking
		standby screen, with even more customisation features. This works great with old phones or
		laptops, as it works across devices. It minimises distractions with a minimal theme.
	</p>
	<h2 class="koulen">The features:</h2>
	<p>
		It allows you to adjust font, font size, accent colour and more! It also features built-in
		screen burn protection, which uses pixel-shifting to minimise damage across displays.
	</p>

	<h2 class="koulen">The code:</h2>
	<p>
		I developed BetterStandby using SvelteKit (my favourite web framework!) and made use of its
		styling and reactivity features across the site to keep it smooth and efficient. Unlike other
		frameworks, Svelte doesn't use a complex render layer, instead compiling into a plain website
		template, which is faster and more efficient for less powerful devices. This project was made
		for HackClub's <a href="https://stardance.hackclub.com/">Stardance event</a>. My final goal is
		to earn a Flipper Zero from Stardance, so if you're able to rate the app on the website well
		(during the short rating period) that would MASSIVELY help me!
	</p>

	<h2 class="koulen">The challenges:</h2>
	<p>
		This project has taught me a lot about some of the weirder bugs across browsers, ranging from
		hallucinating backends to CSS not updating... I also spent a while on an insane bug with nothing
		loading that turned out to just be caused by a single rogue image file being misinterpreted as
		JS at development runtime.
	</p>

	<h2 class="koulen">AI:</h2>
	<p>
		Sure, AI could make this, but where's the fun in that? :D <br /> If I can personally make something
		that helps people, why not try! AI is an amazing tool, but it's not meant to replace you. To put it
		bluntly I only use it for boring stuff I don't need to know. I pointed out every instance of AI code
		usage in my devlogs, so if you want to see, go check those out. I think of programming like an art.
		It's not special when there's no time or effort put into it. AI art is nice and all, but people don't
		only buy art because of how it looks. That's why AI music hasn't replaced human musicians!
	</p>

	<h2 class="koulen">Thank you:</h2>
	<p>
		Thank you for visiting my website! :D I hope you like it and end up finding it useful! I typed
		this all out by hand, so I'm sorry if there are any issues.
	</p>
</div>

<style>
	.fancya {
		background-color: var(--accentColour);
		padding: 3px 10px 5px 10px;
		font-weight: 400;
		box-shadow: inset 0px -5px 0px 0px rgba(0, 0, 0, 0.163);
		border-radius: 30px;
		display: flex;
		color: rgb(0, 0, 0);
		justify-content: center;
		align-items: center;
	}

	a {
		color: var(--accentColour);
		font-weight: 800;
		text-decoration: dashed;
	}
</style>
