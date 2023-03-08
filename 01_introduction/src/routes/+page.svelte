<script lang="ts">
	import Nested from "../components/Nested.svelte";

	const world = 'world';
	let src = '/tutorial/image.gif';
	const name = 'man';
</script>

<h1>Hello {world.toUpperCase()}</h1>
<!-- <img src={src} alt="A {name} dances."> -->
<img {src} alt="A {name} dances." />

<p>This is a paragraph.</p>

<Nested />

<style>
	p {
		color: purple;
		font-family: 'Comic Sans MS', cursive;
		font-size: 2em;
	}
</style>
