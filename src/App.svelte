<script>
  import { onMount } from "svelte";

  let users = [];
  let searchTerm = undefined;
  let filteredMonsters = [];

  onMount(async () => {
    const res = await fetch(
      "https://pokeapi.co/api/v2/pokemon?offset=0&limit=151"
    );
    let user = await res.json();
    users = user.results;
    console.log(users[1]);
  });
  $: filteredMonsters = searchTerm
    ? users.filter((monster) =>
        monster.name.toLocaleLowerCase().includes(searchTerm)
      )
    : users;
</script>

<main>
  <h1>Search Pokemons</h1>
  <input
    class="input is-rounded"
    type="search"
    placeholder="Search Pokemons"
    bind:value={searchTerm}
  />
  <div class="card-list">
    {#each filteredMonsters as user}
      <div class="card">
        <div class="card-image">
          <a href={`https://pokemondb.net/pokedex/${user.name}`}>
            <img
              alt={`${user.name} sprite`}
              src={`https://unpkg.com/pokeapi-sprites@2.0.2/sprites/pokemon/other/dream-world/${user.url.slice(30).replace(/\D/g, "")}.svg`}
              height="200"
              width="200"
            />
          </a>
        </div>
        <h2>{user.name.charAt(0).toUpperCase() + user.name.slice(1)}</h2>
        <p>Pokedex nº {user.url.slice(30).replace(/\D/g, "")}</p>
      </div>
    {/each}
  </div>
</main>

<style>
  @import "https://cdn.jsdelivr.net/npm/bulma@1.0.1/css/bulma.min.css";
  h1 {
    font-size: 3.2em;
    line-height: 1.1;
    margin-top: 50px;
    color: black;
  }
  .card {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    height: 400px;
  }
  .input {
    padding: 10px;
    width: 550px;
    line-height: 30px;
    margin: 70px;
  }
  .card-list {
    width: 85vw;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    grid-gap: 20px;
  }
</style>
