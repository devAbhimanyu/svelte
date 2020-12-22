<script>
import ContactCard from "./components/contactCard/ContactCard.svelte";

  let name = "New";
  let title = "";
  let image = "";
  let description = "";
  let contactList = [];
  let formState = "";
  let id = 0
  
  function createContact(){
	  if(name.trim().length=== 0||title.trim().length=== 0||image.trim().length=== 0||description.trim().length=== 0){
		  formState="invalid";
		  return;
	  }
    contactList=[...contactList,{
      id:`contact${id}`,
      name,
      jobTitle:title,
      imageUrl:image,
      desc:description
    }]
    id+=1;
    // name = "New";
    // title = "";
    // image = "";
    // description = "";
	  formState='done';
  }

  function removeContact(i){
    const list = contactList.splice(i,1);
    contactList = contactList;
  }
</script>

<style>
  #form {
    width: 30rem;
    max-width: 100%;
  }
</style>

<div id="form">
  <div class="form-control">
    <label for="userName">User Name</label>
    <input type="text" bind:value={name} id="userName" />
  </div>
  <div class="form-control">
    <label for="jobTitle">Job Title</label>
    <input type="text" bind:value={title} id="jobTitle" />
  </div>
  <div class="form-control">
    <label for="image">Image URL</label>
    <input type="text" bind:value={image} id="image" />
  </div>
  <div class="form-control">
    <label for="desc">Description</label>
    <textarea rows="3" bind:value={description} id="desc" />
  </div>
  <button on:click="{createContact}">Create Contact</button>
</div>

{#if formState==='invalid'}
<p>Please fill all the fields</p>
{:else}
<p>Enter all values before filling form</p>	
{/if}

<!-- (contact.id) acts as the key, to manage changes -->
{#each contactList as contact,index (contact.id)}
  <h1 on:click="{removeContact.bind(this,index)}"># {index+1}</h1> 
	<ContactCard 
	userName={contact.name} 
	jobTitle={contact.jobTitle} 
	description={contact.desc}
  userImage={contact.imageUrl} />
{:else}
  <p>No contacts found</p>
{/each}
