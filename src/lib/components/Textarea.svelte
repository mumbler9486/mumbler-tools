<script lang="ts">
	export let label: string;
	export let placeholder: string = '';
	export let rows: number = 4;
	export let value: string = '';
</script>

<label class="form-control {$$restProps.class}">
	<div class="label">
		<span class="label-text">{label}</span>
	</div>
	<textarea {rows} class="textarea textarea-bordered" {placeholder} bind:value></textarea>
	<div class="label"></div>
</label>
