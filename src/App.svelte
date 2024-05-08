<script>
  let character = [];
  import Character from "./lib/character.svelte";
  let page = 1;
  async function loadCharecters() {
    const Response = await fetch(
      "https://rickandmortyapi.com/api/character?page=" + page,
    );
    const data = await Response.json();
    character = data.results;
  }
  loadCharecters();

  function nextpage() {
    page++;
    loadCharecters();
  }
  function previouspage() {
    page--;
    loadCharecters();
  }
</script>

<h1 class="title">Rick And Morty</h1>

<div class="conteiner">
  <div class="btns">
    <button class="btn" on:click={previouspage} disabled={page === 1}
      >Regresar</button
    >
    <button class="btn" on:click={nextpage}> Siguiente</button>
  </div>

  <div class="grid">
    {#each character as character}
      <Character {character} />
    {/each}
  </div>
</div>
