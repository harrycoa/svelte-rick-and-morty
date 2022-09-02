<script> 
  let characters = [];

  let page = 1;
  let len = 0;

  async function loadCharacter() {
    const response = await fetch("https://rickandmortyapi.com/api/character?page=" + page);
    const data = await response.json();
    characters = data.results;
    console.log(data);
    len = data.info.count;
    console.log(len);

  }
  loadCharacter();


  // funciones para los botones
  function nextPage() {
    page ++;
    loadCharacter();
  }

  function previousPage(){
    page --;
    loadCharacter();
  }


</script>


<h1>Rick and Morty Svelte</h1>

<button on:click = { previousPage } disabled = { page === 1 }>Previous</button>
<button on:click = { nextPage } disabled = { page === len }>Next</button> 

<br>
<div>

  {#each characters as character }
    <div>
      <img src={character.image} alt={character.name} />
      <h1> {character.name} </h1>
      <h3> {character.species }</h3>
      
    </div>
    
  {/each}

</div>