<script>
	import Keypad from '../../components/Keypad.svelte';

	let pin;
	$: view = pin ? pin.replace(/\d(?!$)/g, '•') : 'enter your pin';

	function handleSubmit() {
		alert(`submitted ${pin}`);
	}

    // Binding to Component instances:
    import InputField from '../../components/InputField.svelte';

    let field
</script>

<h1 style="color: {pin ? '#333' : '#ccc'}">{view}</h1>

<Keypad bind:value={pin} on:submit={handleSubmit} />

<hr />
<!-- Binding to Component Instances -->
<InputField bind:this={field}/>
<button on:click={() => field.focus()}>Focus field</button>