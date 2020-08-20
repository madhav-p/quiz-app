<script>
  import { createEventDispatcher } from "svelte";
  export let corrAnswers = 0;
  const dispatch = createEventDispatcher();
  export let Qno = 0;
</script>

<style>
  header {
    height: 10vh;
    font-size: 2rem;
  }
  header > * {
    margin: 0 0.5em;
  }
  .far {
    color: var(--p-fg);
    cursor: pointer;
  }
  .q-no {
    width: 100%;
    position: relative;
  }
  .progress::before {
    content: "";
    height: 0.6em;
    width: 100%;
    z-index: -1;
    position: absolute;
    top: 50%;
    left: 0;
    transform: translateY(-50%);
    background-color: var(--p-fg);
    border-radius: 0.5em;
  }
  .progress {
    border-radius: 0.5em;
    height: 0.6em;
    width: 50px;
    background-color: rgb(36, 233, 36);
  }
  p {
    font-size: 1.5rem;
  }
</style>

<header class="flex-c-sb">
  <i class="far fa-arrow-alt-circle-left" on:click={() => dispatch('exit')} />
  <div class="q-no">
    <div class="progress" style="width:{(Qno * 100) / 10}%" />
  </div>
  <p>Pts:{corrAnswers}/10</p>
  <!-- <i class="far fa-times-circle" /> -->
</header>
