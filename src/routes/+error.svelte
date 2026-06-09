<script lang="ts">
	import { page } from '$app/state';
</script>

<div class="centerdiv">
	<img src="/capybara.png" alt="A bored sitting capybara" />
	<h1>{page.error?.message}!</h1>
	<div class="divider mb-2"></div>
	<p>Please check that the link is correct. Otherwise continue staring at Jeffrey the capybara.</p>
	<p class="mb-5">If you think this is an issue, please contact Capy (me) on Slack. :D</p>
</div>
