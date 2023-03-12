<script>
	let numbers = [1, 2, 3, 4];

	function addNumber() {
		// numbers.push(numbers.length + 1);
		// // console.log(numbers);
		// assign numbers to itself to trigger exection of sum function
		// because .push(), pop(), .shift(), .splice(), .set(), .add(),...
		// don't trigger reactivity => they are not a reassignment
		// numbers = numbers
		// ES6 way of doing it:
		numbers = [...numbers, numbers.length + 1];
		// A simple rule of thumb for reactivity:
		// the updated variable must directly appear
		// on the left hand side of the assignment.
	}

	$: sum = numbers.reduce((t, n) => t + n, 0);
</script>

<p>{numbers.join(' + ')} = {sum}</p>

<button on:click={addNumber}>
	Add a number
</button>