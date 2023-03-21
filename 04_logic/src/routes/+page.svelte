<script>
	let user = { loggedIn: false };

	function toggle() {
		user.loggedIn = !user.loggedIn;
	}

    let x = 7

    let cats = [
        { id: 'J---aiyznGQ', name: 'Keyboard Cat' },
		{ id: 'z_AbfPXTKms', name: 'Maru' },
		{ id: 'OUtn3pvWmpg', name: 'Henri The Existential Cat' }
    ]

    import Thing from '../components/Thing.svelte';

	let things = [
		{ id: 1, name: 'apple' },
		{ id: 2, name: 'banana' },
		{ id: 3, name: 'carrot' },
		{ id: 4, name: 'doughnut' },
		{ id: 5, name: 'egg' },
	];

	function handleClick() {
		things = things.slice(1);
	}
</script>

<!-- {#if user.loggedIn}
<button on:click={toggle}>
	Log out
</button>
{/if}

{#if !user.loggedIn}
<button on:click={toggle}>
	Log in
</button>
{/if} -->

{#if user.loggedIn}
<button on:click={toggle}>
	Log out
</button>
{:else}
<button on:click={toggle}>
	Log in
</button>
{/if}

<!-- A # character always indicates a block opening tag. A / character always indicates a block closing tag. A : character, as in {:else}, indicates a block continuation tag. Don't worry — you've already learned almost all the syntax Svelte adds to HTML. -->

<hr/>

{#if x > 10}
<p>{x} is greater than 10</p>
{:else if x < 5}
<p>{x} is less than 5</p>
{:else}
<p>{x} is between 5 and 10</p>
{/if}

<hr/>

<h1>The Famous Cats of YouTube</h1>

<!-- <ul>
	{#each cats as cat}
		<li><a target="_blank" href="https://www.youtube.com/watch?v={cat.id}" rel="noreferrer">
			{cat.name}
		</a></li>
	{/each}
</ul> -->

<!-- adding index: -->

<!-- <ul>
	{#each cats as cat, idx}
		<li><a target="_blank" href="https://www.youtube.com/watch?v={cat.id}" rel="noreferrer">
			{idx + 1}: {cat.name}
		</a></li>
	{/each}
</ul> -->

<!-- using destructuring: -->

<ul>
	{#each cats as {id, name}, idx}
		<li><a target="_blank" href="https://www.youtube.com/watch?v={id}" rel="noreferrer">
			{idx + 1}: {name}
		</a></li>
	{/each}
</ul>

<hr/>

<!-- Example why key is needed:-->
<!-- 
<button on:click={handleClick}>
	Remove first thing
</button>

{#each things as thing}
	<Thing name={thing.name}/>
{/each} -->

<!-- Adding key fixes issue: -->

<button on:click={handleClick}>
	Remove first thing
</button>

{#each things as thing (thing.id)}
<Thing name={thing.name}/>
{/each}

<!-- You can use any object as the key, as Svelte uses a Map internally — in other words you could do (thing) instead of (thing.id). Using a string or number is generally safer, however, since it means identity persists without referential equality, for example when updating with fresh data from an API server.-->
