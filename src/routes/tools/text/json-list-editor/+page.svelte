<script lang="ts">
	import Textarea from '$lib/components/Textarea.svelte';

	let list: string = '';
	let jsonList: string = '[]';

	let isTextFocused: boolean = false;
	let isJsonFocused: boolean = false;

	let jsonError: string = '';

	$: convertToJson(list);
	$: convertToText(jsonList);

	const convertToJson = (rawList: string) => {
		// List to JSON
		if (!isTextFocused) {
			return;
		}

		const itemList = rawList.split('\n');

		if (itemList.length > 0 && itemList[0] === '') {
			jsonList = '[]';
		} else {
			jsonList = itemList.length > 0 && itemList[0] ? JSON.stringify(itemList, null, 2) : '[]';
		}
		jsonError = '';
	};

	const convertToText = (rawJson: string) => {
		// JSON to list
		if (!isJsonFocused) {
			return;
		}

		try {
			const listRaw = JSON.parse(rawJson) as string[];
			list = listRaw.join('\n');
			jsonError = '';
		} catch (err) {
			jsonError = (err as Error).toString();
			console.error(err);
		}
	};

	const textInputPressed = () => {
		isTextFocused = true;
		isJsonFocused = false;
	};

	const jsonInputPressed = () => {
		isTextFocused = false;
		isJsonFocused = true;
	};
</script>

<div class="flex w-full">
	<Textarea
		class="w-1/2"
		rows={30}
		label="Enter a newline separated list of items:"
		bind:value={list}
		on:input={textInputPressed}
	/>
	<div class="divider divider-horizontal"></div>
	<Textarea
		class="w-1/2"
		rows={30}
		label="JSON List"
		bind:value={jsonList}
		on:input={jsonInputPressed}
		error={jsonError}
	/>
</div>
