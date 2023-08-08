<script>
	let name = 'world';

    // Numeric inputs:
    let a = 1
    let b = 2

    // Checkbox inputs:
    let yes = false

    // Grouping inputs:
    let menu = ['Cookies and cream', 'Mint choc chip', 'Raspberry ripple']
    let scoops = 1
	let flavours = ['Mint choc chip']

	function join(flavours) {
		if (flavours.length === 1) return flavours[0]
		return `${flavours.slice(0, -1).join(', ')} and ${flavours[flavours.length - 1]}`
	}

    // Textarea inputs:
    import { marked } from 'marked'
    let value = `Some words are *italic*, some are **bold**`

    // Select bindings:
    let questions = [
		{ id: 1, text: `Where did you go to school?` },
		{ id: 2, text: `What is your mother's name?` },
		{ id: 3, text: `What is another personal fact that an attacker could easily find with Google?` }
	];

	let selected;

	let answer = '';

	function handleSubmit() {
		alert(`answered question ${selected.id} (${selected.text}) with "${answer}"`);
	}

    //Select multiple:
    let scoops_multiple = 1;
	let flavours_multiple = ['Mint choc chip'];

	let menu_multiple = ['Cookies and cream', 'Mint choc chip', 'Raspberry ripple'];

	function join_multiple(flavours) {
		if (flavours.length === 1) return flavours[0];
		return `${flavours.slice(0, -1).join(', ')} and ${flavours[flavours.length - 1]}`;
	}

    // Contenteditable bindings:
    let html = '<p>Write some text!</p>';

    // Each block bindings:
    let todos = [
		{ done: false, text: 'finish Svelte tutorial' },
		{ done: false, text: 'build an app' },
		{ done: false, text: 'world domination' }
	];

	function add() {
		todos = todos.concat({ done: false, text: '' });
	}

	function clear() {
		todos = todos.filter((t) => !t.done);
	}

	$: remaining = todos.filter((t) => !t.done).length;
</script>

<input bind:value={name} />

<h1>Hello {name}!</h1>

<hr />
<!-- Numeric inputs: -->
<label>
	<input type="number" bind:value={a} min="0" max="10" />
	<input type="range" bind:value={a} min="0" max="10" />
</label>

<label>
	<input type="number" bind:value={b} min="0" max="10" />
	<input type="range" bind:value={b} min="0" max="10" />
</label>

<p>{a} + {b} = {a + b}</p>

<hr />
<!-- Checkbox inputs: -->
<label>
    <input type="checkbox" bind:checked={yes} />
    Yes! Send me regular email spam.
</label>

{#if yes}
    <p>Thank you. We will bombard your inbox and sell your personal details.</p>
{:else}
    <p>You must opt-in to continue. If you are not paying, you're the product.</p>
{/if}

<hr />
<!-- Group inputs: -->
<h2>Size</h2>

<label>
	<input type="radio" bind:group={scoops} name="scoops" value={1} />
	One scoop
</label>

<label>
	<input type="radio" bind:group={scoops} name="scoops" value={2} />
	Two scoops
</label>

<label>
	<input type="radio" bind:group={scoops} name="scoops" value={3} />
	Three scoops
</label>

<h2>Flavours</h2>

<!-- <label>
	<input type="checkbox" bind:group={flavours} name="flavours" value="Cookies and cream" />
	Cookies and cream
</label>

<label>
	<input type="checkbox" bind:group={flavours} name="flavours" value="Mint choc chip" />
	Mint choc chip
</label>

<label>
	<input type="checkbox" bind:group={flavours} name="flavours" value="Raspberry ripple" />
	Raspberry ripple
</label> -->
{#each menu as flavour}
<label>
    <input type="checkbox" bind:group={flavours} name="flavour" value={flavour} />
    {flavour}
</label>
{/each}

{#if flavours.length === 0}
	<p>Please select at least one flavour</p>
{:else if flavours.length > scoops}
	<p>Can't order more flavours than scoops!</p>
{:else}
	<p>
		You ordered {scoops}
		{scoops === 1 ? 'scoop' : 'scoops'}
		of {join(flavours)}
	</p>
{/if}

<hr />
<!-- Textarea inputs: -->
<!-- Consider using DOMPurify / sanitizer in connection with marked! Strips off all dangerous HTML to prevent cross-site-scripting (CSS) -->
{@html marked(value)}
<!-- <textarea bind:value={value}></textarea> -->
<textarea bind:value />

<hr />
<!-- Select bindings: -->
<h2>Insecurity questions</h2>

<form on:submit|preventDefault={handleSubmit}>
	<select bind:value={selected} on:change={() => (answer = '')}>
		{#each questions as question}
			<option value={question}>
				{question.text}
			</option>
		{/each}
	</select>

	<input class="select" bind:value={answer} />

	<button disabled={!answer} type="submit"> Submit </button>
</form>

<p>selected question {selected ? selected.id : '[waiting...]'}</p>

<hr />
<!-- Select multiple -->
<h2>Size</h2>

<label>
	<input type="radio" bind:group={scoops_multiple} value={1} />
	One scoop
</label>

<label>
	<input type="radio" bind:group={scoops_multiple} value={2} />
	Two scoops
</label>

<label>
	<input type="radio" bind:group={scoops_multiple} value={3} />
	Three scoops
</label>

<h2>Flavours</h2>

<!-- {#each menu as flavour}
	<label>
		<input type="checkbox" bind:group={flavours_multiple} value={flavour} />
		{flavour}
	</label>
{/each} -->

<select multiple bind:value={flavours_multiple}>
    {#each menu_multiple as flavour}
        <option value={flavour}>
            {flavour}
        </option>
    {/each}
</select>

{#if flavours_multiple.length === 0}
	<p>Please select at least one flavour</p>
{:else if flavours_multiple.length > scoops_multiple}
	<p>Can't order more flavours than scoops!</p>
{:else}
	<p>
		You ordered {scoops_multiple}
		{scoops_multiple === 1 ? 'scoop' : 'scoops'}
		of {join(flavours_multiple)}
	</p>
{/if}

<hr />
<!-- Contenteditable bindings: -->
<div contenteditable="true" bind:innerHTML={html}/>

<pre>{html}</pre>

<hr />
<!-- Each block bindings: -->
<!-- Note that interacting with these <input> elements will mutate the array. 
    If you prefer to work with immutable data, you should avoid these bindings
    and use event handlers instead. -->
<h1>Todos</h1>

{#each todos as todo}
	<div class:done={todo.done}>
		<input type="checkbox" bind:checked={todo.done} />

		<input placeholder="What needs to be done?" bind:value={todo.text} />
	</div>
{/each}

<p>{remaining} remaining</p>

<button on:click={add}> Add new </button>

<button on:click={clear}> Clear completed </button>

<hr />

<style>
	label {
		display: flex;
	}
	input,
	p {
		margin: 6px;
	}
    input.select {
		display: block;
		width: 500px;
		max-width: 100%;
	}
    [contenteditable] {
		padding: 0.5em;
		border: 1px solid #eee;
		border-radius: 4px;
	}
    .done {
		opacity: 0.4;
	}
</style>