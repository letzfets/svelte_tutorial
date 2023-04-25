<script>
	let m = { x: 0, y: 0 };

	function handleMousemove(event) {
		m.x = event.clientX;
		m.y = event.clientY;
	}

    // demonstrates modifiers:
    function handleClick() {
        alert('clicked')
    }

    // component events:
    import Inner from './Inner.svelte';

	function handleMessage(event) {
		// console.log(event)
		alert(event.detail.text);
	}

	// event forwarding:
	import Outer from './Outer.svelte'

	function handleMessageOuter(event){
		// console.log(event.detail)
		alert(event.detail.text)
	}

	// DOM event forwarding:
	import CustomButton from './CustomButton.svelte'

	function handleClickDOM() {
		alert('Button clicked')
	}
</script>

<div on:mousemove={handleMousemove}>
	The mouse position is {m.x} x {m.y}
</div>

<div on:mousemove="{e => m = { x: e.clientX, y: e.clientY }}">
	The mouse position is {m.x} x {m.y}
</div>

<!-- modifier demonstration -->
<button on:click|once={handleClick}>
	Click me
</button>

<style>
	div { width: 100%; height: 100%; }
</style>
<br>

<!-- Component events demonstration -->
<Inner on:message={handleMessage}/>
<br>

<!-- Event forwarding demonstration -->
<Outer on:message={handleMessageOuter}/>
<br>

<!-- DOM event forwarding demonstration -->
<CustomButton on:click={handleClickDOM}/>