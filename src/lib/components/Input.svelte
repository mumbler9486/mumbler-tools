<script lang="ts">
	export let placeholder: string = '';
	export let value: string = '';
	export let label: string = '';
	export let maxlength: number = 5000;
	export let error: string | undefined = '';
</script>

<div class="form-control w-full max-w-xs">
	<label class="label" for="input">
		<span class="label-text">{label}</span>
	</label>
	<input
		type="text"
		{placeholder}
		class="input input-bordered w-full max-w-xs"
		{maxlength}
		bind:value
	/>
	{#if !!error && error !== ''}
		<label class="label" for="input">
			<span class="label-text text-error">{error}</span>
		</label>
	{/if}
</div>
