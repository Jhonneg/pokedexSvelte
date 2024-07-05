<script>
	import { onMount } from 'svelte';

	let users = [];

	onMount(async () => {
		const res = await fetch(`https://jsonplaceholder.typicode.com/users`);
		users = await res.json();
	});
</script>

<main>
 <h1>Search Monsters</h1>
<input
      class="search-box"
      type="search"
      placeholder="Search Monsters"
    />

		<div class="card-list">
	{#each users as user}
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