<script>
	import Modal from './Modal.svelte';
	import AddPersonForm from './AddPersonForm.svelte'

	let showModal = false;

  let people = [
		{ name: 'yoshi', beltColour: 'black', age: 25, id: 1 },
		{ name: 'mario', beltColour: 'orange', age: 45, id: 2 },
		{ name: 'luigui', beltColour: 'brown', age: 35, id: 3 }
	];

	const chandleClick = (personId) => {
		people = people.filter(person => person.id !== personId)
	}

	const toggleModal = () => {
		showModal = !showModal;
	}

	const addPerson = (e) => {
		// console.log('e ==>', e.detail)
		const person = e.detail
		people = [person, ...people]
	}
</script>

<Modal {showModal} on:click={toggleModal}>
	<AddPersonForm on:addPerson={addPerson} />
</Modal>
<main>
	<button on:click={toggleModal}>Open Modal</button>
	{#each people as person (person.id)}
		<div>
			<h4>{person.name}</h4>
			<p>{person.age} years old, {person.beltColour} belt.</p>
			{#if person.beltColour === 'black'}
				<p><strong>MASTER NINJAS</strong></p>
			{/if}
			<button on:click={() => chandleClick(person.id)}>Delete</button>
		</div>
		{:else}
			<p>There are no people to show</p>
	{/each}
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

