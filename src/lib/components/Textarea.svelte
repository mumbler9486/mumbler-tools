<script lang="ts">
	export let label: string;
	export let error: string = '';
	export let placeholder: string = '';
	export let rows: number = 4;
	export let value: string = '';
	export let readonly: boolean = false;
</script>

<label class="form-control {$$restProps.class}">
	<div class="label">
		<span class="label-text">{label}</span>
	</div>
	<textarea
		{rows}
		class="textarea textarea-bordered leading-tight"
		{placeholder}
		{readonly}
		bind:value
		on:input
	/>
	<div class="label text-xs text-error">{error}</div>
</label>
