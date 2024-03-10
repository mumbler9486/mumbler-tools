<script lang="ts">
	import Input from '$lib/components/Input.svelte';
	import Textarea from '$lib/components/Textarea.svelte';

	const MaxIterations = 1_000_000;
	const MinInt = -1_000_000;
	const MaxInt = 1_000_000;

	let minNumberRaw = '1';
	let maxNumberRaw = '100';
	let stepRaw = '1';

	let minNumberError = '';
	let maxNumberError = '';
	let stepNumberError = '';
	let error = '';

	$: minNumber = parseFloat(minNumberRaw);
	$: maxNumber = parseFloat(maxNumberRaw);
	$: stepNumber = parseFloat(stepRaw);

	$: numListDisplay = generateNumbers(minNumber, maxNumber, stepNumber)?.join('\n') ?? '';

	const generateNumbers = (min: number, max: number, step: number) => {
		minNumberError = '';
		maxNumberError = '';
		stepNumberError = '';
		error = '';
		numListDisplay = '';

		console.log('Generating numbers: (min, max, step)', min, max, step);

		if (isNaN(min)) {
			minNumberError = 'Value is NaN.';
		}

		if (isNaN(max)) {
			maxNumberError = 'Value is NaN.';
		}

		if (isNaN(step)) {
			stepNumberError = 'Value is NaN.';
		}

		if (min >= MaxInt || min <= MinInt) {
			minNumberError = `Min must be between ${MinInt.toLocaleString()} and ${MaxInt.toLocaleString()}`;
		}

		if (max >= MaxInt || max <= MinInt) {
			maxNumberError = `Max must be between ${MinInt.toLocaleString()} and ${MaxInt.toLocaleString()}`;
		}

		if (step >= MaxInt || step <= MinInt) {
			stepNumberError = `Step must be between ${MinInt.toLocaleString()} and ${MaxInt.toLocaleString()}`;
		}

		if (step <= 0) {
			stepNumberError = 'Cannot have a step of zero or negative';
		}

		if (max < min) {
			minNumberError = 'Min cannot be greater than Max';
		}

		if (max - min === 0) {
			error = 'Nothing to generate';
		}

		// Some errors exist do not proceed
		if (minNumberError !== '' || maxNumberError !== '' || stepNumberError !== '') {
			return;
		}

		const numList = [];
		let iterationCount = 0;
		for (let i = min; i <= max; i += step) {
			iterationCount++;
			numList.push(i);

			if (iterationCount > MaxIterations) {
				error = `Max Iterations of ${MaxIterations.toLocaleString()} exceeded. Check step count. Stopping generation`;
				console.error(error);
				return numList;
			}
		}

		return numList;
	};
</script>

<div class="flex w-full">
	<div class="w-1/2">
		<Input
			label="Starting number"
			maxlength={25}
			error={minNumberError}
			bind:value={minNumberRaw}
		/>
		<Input label="Ending number" maxlength={25} error={maxNumberError} bind:value={maxNumberRaw} />
		<Input label="Step" maxlength={25} error={stepNumberError} bind:value={stepRaw} />
	</div>
	<div class="divider divider-horizontal"></div>
	<Textarea class="w-1/2" rows={30} label="Output" readonly {error} bind:value={numListDisplay} />
</div>
