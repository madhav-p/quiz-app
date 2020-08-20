<script>
  import Quiz from "./Quiz.svelte";
  let category = 0;
  const subjects = [
    {
      name: "General Knowledge",
      category: 9,
    },
    {
      name: "Mathematics",
      category: 19,
    },
    {
      name: "Computers",
      category: 18,
    },
    {
      name: "History",
      category: 23,
    },
  ];
</script>

<style>
  main {
    width: 100%;
    max-width: 800px;
    margin: 0 auto;

    display: grid;
    grid-template-rows: max-content 1fr;
  }
  ul {
    margin: 1em 0;
    display: grid;
    gap: 1em;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  }
  h1 {
    font-size: 3rem;
    text-align: center;
    padding: 0.5em 1em;
  }
  li {
    cursor: pointer;
    font-size: 1.7rem;
    text-align: center;
  }
</style>

<main>
  {#if category}
    <Quiz {category} on:exit={() => (category = 0)} />
  {:else}
    <h1>Choose your Subject</h1>
    <ul>
      {#each subjects as subject}
        <li class="card" on:click={() => (category = subject.category)}>
          {subject.name}
        </li>
      {/each}
    </ul>
  {/if}

</main>
