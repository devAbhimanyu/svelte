<script>
	import ContactCard from './components/compCard/ContactCard.svelte';
	let name = 'Max';
	let age = 30;
	let error = "";
	/**
	 * this is called a labeled statement, which has been used by svelte, for dynamic value updation
	 * when a variable values changes, it will automatically trigger the event to update the labeled statement
	 * it is best practice to have these labebel variables configured for dynamic values, rather than in the markup
	 */
	$: uppercaseName = name.toUpperCase()

	$: error = age>34?"you are old":""

	function incrementAge() {
		age += 1;
	}
	function changeName(){
		name="Neilta"
	}

	function inputHandler(e){
		const {value} = e.target;
		console.log(value)
		name=value;
	}
</script>

<style>
	h1 {
		color: purple;
	}
</style>

<h1>Hello {uppercaseName}, my age is {age}!</h1>
<button on:click="{incrementAge}">Change Age</button>
<button on:click="{changeName}">Change name</button>
<!-- bind is used for two way binding, it is not recommended and there should be a reason for using this-->
<!-- <input type="text" bind:value={name}> -->
<!-- uni direction data binding is similar to react, use react -->
<input type="text" value="{name}" on:input="{inputHandler}">
<p>{error}</p>
<ContactCard userName="{name}"/>
