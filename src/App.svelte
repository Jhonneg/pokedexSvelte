<script>
  import { onMount } from "svelte";

  let users = [];
  let searchTerm = undefined;
  let filteredMonsters = [];

  onMount(async () => {
    const res = await fetch(`https://jsonplaceholder.typicode.com/users`);
    users = await res.json();
  });
  $: filteredMonsters = searchTerm
    ? users.filter((monster) =>
        monster.name.toLocaleLowerCase().includes(searchTerm)
      )
    : users;
</script>

<main>
  <h1>Search Monsters</h1>
  <input
    class="search-box"
    type="search"
    placeholder="Search Monsters"
    bind:value={searchTerm}
  />
  <div class="card-list">
    {#each filteredMonsters as user}
      <div class="card-container">
        <img
          alt={`monster ${user.name}`}
          src={`https://robohash.org/${user.id}?set=set2&size=180x180`}
        />
        <h2>{user.name}</h2>
        <p>{user.email}</p>
      </div>
    {/each}
  </div>
</main>

<style>
  h1 {
    font-size: 3.2em;
    line-height: 1.1;
  }
  .search-box {
    border: none;
    outline: none;
    padding: 10px;
    width: 150px;
    line-height: 30px;
    margin-bottom: 30px;
  }
  .card-list {
    width: 85vw;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    grid-gap: 20px;
  }
  .card-container {
    display: flex;
    flex-direction: column;
    background-color: #95dada;
    border: 1px solid grey;
    border-radius: 5px;
    padding: 25px;
    cursor: pointer;
    -moz-osx-font-smoothing: grayscale;
    backface-visibility: hidden;
    transform: translateZ(0);
    transition: transform 0.25s ease-out;
  }
  .card-container:hover {
    transform: scale(1.05);
  }
</style>
