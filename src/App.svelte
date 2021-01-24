<script>
  import Modal from './Modal.svelte';
  import AddPersonForm from './AddPersonForm.svelte';

  let showModal = false;

  let people = [
    { name: 'yoshi', beltColor: 'black', age: 25, id: 1 },
    { name: 'mario', beltColor: 'orange', age: 45, id: 2 },
    { name: 'luigi', beltColor: 'brown', age: 35, id: 3 },
  ];

  const handleDelete = (id) => {
    people = people.filter((person) => person.id !== id);
  };

  const toggleModal = () => {
    showModal = !showModal;
  };

  const addPerson = (e) => {
    const person = e.detail;
    people = [person, ...people];
    showModal = false;
  };
</script>

<Modal {showModal} on:click={toggleModal}>
  <AddPersonForm on:addPerson={addPerson} />
</Modal>

<main>
  <button on:click={toggleModal}>Open Modal</button>
  <h1>Hello Svelte!</h1>
  {#each people as person (person.id)}
    <div>
      <h4>{person.name}</h4>
      <p>{person.age} years old, {person.beltColor} belt.</p>
      <button
        on:click={() => {
          handleDelete(person.id);
        }}>delete</button
      >
    </div>
  {:else}
    <h2>Nothing to show.</h2>
  {/each}
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
