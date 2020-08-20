<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();
  export let Ques = {};
  export let Qno = 0;
  let isSubmitted = false;

  const handleSubmit = (sel, corr) => {
    isSubmitted = true;
    if (sel == corr) {
      dispatch("incrCorr");
    }
  };
</script>

<style>
  .card {
    padding: 3em;
    text-align: center;
  }
  ul {
    margin: 2em 0;
    font-size: 1.1rem;
  }
  ul > * {
    margin-top: 0.5em;
  }
  li {
    justify-content: center;
    padding: 0.5em 1em;
    cursor: pointer;
    background-color: lightgray;
    border-radius: 0.5em;
  }
  li:hover {
    background-color: rgb(158, 178, 197);
  }
  p {
    text-align: center;
  }
  .selected {
    background-color: var(--dis);
  }
  .correct {
    background-color: limegreen;
  }
  .incorrect {
    background-color: firebrick;
  }
  .btns {
    justify-content: center;
  }
  button {
    cursor: pointer;
    text-transform: uppercase;
    background-color: var(--p-bg);
    color: var(--p-fg);
    padding: 1em 2em;
    letter-spacing: 1px;
    border: none;
    border-radius: 10px;
  }
  /* button:disabled {
    background-color: var(--dis);
    cursor: initial;
  } */
</style>

<div class="card">
  <h1>
    {@html Ques.question}
  </h1>
  <ul>
    {#each Ques.options as option}
      <li
        class="flex"
        on:click={() => (Ques.selectedOption = option)}
        class:selected={Ques.selectedOption == option}
        class:incorrect={(Ques.selectedOption == option) & (option != Ques.correct_answer) & isSubmitted}
        class:correct={(option == Ques.correct_answer) & isSubmitted}>
        <p>
          {@html option}
        </p>
      </li>
    {/each}
  </ul>
  <div class="flex btns">
    {#if !isSubmitted}
      <button
        class="submit"
        on:click|once={() => handleSubmit(Ques.selectedOption, Ques.correct_answer)}>
        Submit
      </button>
    {:else if Qno == 10}
      <button class="finish">Finish Quiz</button>
    {:else}
      <button class="next" on:click={() => dispatch('gotoNextQues')}>
        Next
      </button>
    {/if}
  </div>
</div>
