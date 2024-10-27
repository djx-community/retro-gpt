<script lang="ts">
	import { onMount } from 'svelte';
	import LoadingScreen from '$lib/LoadingScreen.svelte';
	import MainApp from '$lib/App.svelte';

	let showLoading = true;

	onMount(() => {
		setTimeout(() => {
			showLoading = false;
		}, 6000); // 7 seconds loading screen
	});
</script>

{#if showLoading}
	<LoadingScreen />
{:else}
	<div class="transition-opacity duration-500">
		<MainApp />
	</div>
{/if}
