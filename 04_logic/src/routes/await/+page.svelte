<script>
	async function getRandomNumber() {
		const res = await fetch(`/tutorial/random-number`);// missing in tutorial
		const text = await res.text();

		if (res.ok) {
			return text;
		} else {
			throw new Error(text);
		}
	}

	let promise = getRandomNumber();

	function handleClick() {
		promise = getRandomNumber();
	}
</script>

<button on:click={handleClick}>
	generate random number
</button>

{#await promise}
<p>...waiting</p>
{:then number}
<p>The number is {number}</p>
{:catch error}
<p style="color: red">{error.message}</p>
{/await}

<!-- For promisses, that cannot be rejected and don't have a placeholder while waiting: -->
<!-- {#await promise then number}
	<p>the number is {number}</p>
{/await} -->