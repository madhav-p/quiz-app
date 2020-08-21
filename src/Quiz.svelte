<script>
  import Header from "./Header.svelte";
  import Question from "./Question.svelte";
  import Loading from "./Loading.svelte";
  import Finished from "./Finished.svelte";

  let corrAnswers = 0;
  export let category = 0;
  let Quiz = [];
  let currQuesNo = 1;
  let finished = false;
  const shuffle = (array) => {
    array.sort(() => Math.random() - 0.5);
  };
  const computeUrl = (category) =>
    `https://opentdb.com/api.php?amount=10&category=${category}`;

  const fetchQuiz = (url) => {
    fetch(url)
      .then((res) => res.json())
      .then((data) => {
        data.results.forEach((d) => {
          d.options = [...d.incorrect_answers, d.correct_answer];
          shuffle(d.options);
          d.selectedOption = null;
        });
        Quiz = data.results;
      })
      .catch((e) => console.log(e));
  };

  fetchQuiz(computeUrl(category));
</script>

{#if finished}
  <Finished {corrAnswers} />
{:else}
  <Header Qno={currQuesNo} on:exit {corrAnswers} />
  {#each Quiz as Q, i}
    {#if currQuesNo === i + 1}
      <Question
        Ques={Q}
        Qno={currQuesNo}
        on:finish={() => (finished = true)}
        on:incrCorr={() => corrAnswers++}
        on:gotoNextQues={() => currQuesNo++}
        on:gotoPrevQues={() => currQuesNo--} />
    {/if}
  {:else}
    <Loading />
  {/each}
{/if}
