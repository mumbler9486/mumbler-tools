<script lang="ts">
	export let label: string;
	export let placeholder: string = '';

	export let value: string = '';
</script>

<label class="form-control {$$restProps.class}">
	<div class="label">
		<span class="label-text">{label}</span>
	</div>
	<textarea rows="20" cols="40" class="textarea textarea-bordered h-24" {placeholder} bind:value
	></textarea>
	<div class="label"></div>
</label>
