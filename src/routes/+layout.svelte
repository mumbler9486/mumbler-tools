<script lang="ts">
	import Navigation from '$lib/components/Navigation.svelte';
	import '../app.css';
</script>

<main>
	<Navigation>
		<div class="p-4">
			<slot />
		</div>
	</Navigation>
</main>
