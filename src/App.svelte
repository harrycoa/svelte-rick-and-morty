<script>
  import Character from "./lib/Character.svelte";
  let characters = [];

  let page = 1;
  let len = 0;

  async function loadCharacter() {
    const response = await fetch(
      "https://rickandmortyapi.com/api/character?page=" + page
    );
    const data = await response.json();
    characters = data.results;
    console.log(data);
    len = data.info.count;
    console.log(len);
  }
  loadCharacter();

  // funciones para los botones
  function nextPage() {
    page++;
    loadCharacter();
  }

  function previousPage() {
    page--;
    loadCharacter();
  }
</script>

<h1 class="title">Rick and Morty Svelte</h1>



<br />
<div class="container">
  <div class="btns">
    <button class="btn" on:click={previousPage} disabled={page === 1}>Previous</button>
    <button class="btn" on:click={nextPage} disabled={page === len}>Next</button>
  </div>
  <br>  
  <div class="grid">
    {#each characters as character}
      <Character {character} />
    {/each}
  </div>
</div>
