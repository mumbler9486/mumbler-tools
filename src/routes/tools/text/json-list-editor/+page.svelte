<script lang="ts">
	import Textarea from '$lib/components/Textarea.svelte';

	let list: string = '';
	let jsonList: string = '';

	$: {
		const itemList = list.split('\n');

		if (itemList.length > 0 && itemList[0] === '') {
			jsonList = '[]';
		} else {
			jsonList = itemList.length > 0 && itemList[0] ? JSON.stringify(itemList, null, 2) : '[]';
		}
	}
</script>

<div class="flex w-full">
	<Textarea
		class="w-1/2"
		rows={18}
		label="Enter a comma separated list of items:"
		bind:value={list}
	/>
	<div class="divider divider-horizontal"></div>
	<Textarea class="w-1/2" rows={18} label="JSON List" bind:value={jsonList} />
</div>
