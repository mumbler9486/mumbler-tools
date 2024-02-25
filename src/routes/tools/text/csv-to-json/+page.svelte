<script lang="ts">
	import Textarea from '$lib/components/Textarea.svelte';

	let list: string = '';
	let jsonList: Record<string, string>[] = [];

	let error: string = '';

	$: convertToJson(list);

	const convertToJson = (rawList: string) => {
		error = '';

		const rowList = rawList.split('\n');

		if (rowList.length > 0 && rowList[0] === '') {
			jsonList = [];
		} else {
			jsonList = convertToArray(rowList);
		}
	};

	const convertToArray = (rawList: string[]): Record<string, string>[] => {
		if (rawList.length <= 0) {
			return [];
		}

		const headerRow = rawList[0].split(',');
		if (rawList.length == 1) {
			return [];
		}

		const jsonArray: Record<string, string>[] = [];
		for (const rawRow of rawList.splice(1)) {
			const splittedRow = rawRow.split(',');
			jsonArray.push(reduceStringArrayToObject(headerRow, splittedRow));
		}

		return jsonArray;
	};

	const reduceStringArrayToObject = (headers: string[], row: string[]) => {
		if (headers.length != row.length) {
			console.warn('This row has different number of columns than headers', headers, row);
			error = 'A row has different number of columns than headers was detected';
		}

		return row.reduce(
			(prev, curr, i) => {
				if (!headers[i]) {
					// Skip if columns more than headers
					return prev;
				}
				prev[headers[i].trim()] = curr;
				return prev;
			},
			{} as Record<string, string>
		);
	};
</script>

<div class="flex w-full">
	<Textarea
		class="w-1/2"
		rows={18}
		label="Enter rows comma separated. First row is the header row."
		bind:value={list}
		{error}
	/>
	<div class="divider divider-horizontal"></div>
	<Textarea class="w-1/2" rows={18} label="JSON" readonly value={JSON.stringify(jsonList)} />
</div>
