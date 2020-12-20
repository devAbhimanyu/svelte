<script>
  import ContactCard from "./components/compCard/ContactCard.svelte";

  let name = "abc";
  let title = "";
  let image = "";
  let description = "";
  let age = 30;


  /**
   * this is called a labeled statement, which has been used by svelte, for dynamic value updation
   * when a variable values changes, it will automatically trigger the event to update the labeled statement
   * it is best practice to have these labebel variables configured for dynamic values, rather than in the markup
   */
  $: uppercaseName = name.toUpperCase();

  $: console.log(name);

  function incrementAge() {
    age += 1;
  }


  function inputHandler(event) {
    const enteredValue = event.target.value;
    name = enteredValue;
  }
</script>

<style>
  h1 {
    color: purple;
  }
</style>

<h1>Hello {uppercaseName}, my age is {age}!</h1>
<button on:click={incrementAge}>Change Age</button>
<!-- bind is used for two way binding, it is not recommended and there should be a reason for using this-->
<!-- <input type="text" bind:value={name}> -->
<!-- uni direction data binding is similar to react, use react -->
<!-- <input type="text" value="{name}" on:input="{inputHandler}"> -->
<input type="text" bind:value={name} />
<input type="text" bind:value={title} />
<input type="text" bind:value={image} />
<textarea rows="3" bind:value={description} />

<ContactCard 
	userName={name} 
	jobTitle={title} 
	{description} 
	userImage={image} />
